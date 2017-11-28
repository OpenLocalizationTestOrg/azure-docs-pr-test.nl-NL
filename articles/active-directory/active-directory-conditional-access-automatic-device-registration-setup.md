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
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="66120-103">Hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66120-103">How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="66120-104">toouse [voorwaardelijke toegang voor Azure Active Directory op basis van apparaten](active-directory-conditional-access-azure-portal.md), uw computers moeten worden geregistreerd bij Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="66120-104">toouse [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="66120-105">U kunt een lijst met geregistreerde apparaten krijgen in uw organisatie met behulp van Hallo [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in Hallo [Azure Active Directory PowerShell-module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="66120-105">You can get a list of registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="66120-106">Dit artikel bevat Hallo stappen voor het configureren van automatische registratie van Windows-domein apparaten Hallo met Azure AD in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="66120-106">This article provides you with hello steps for configuring hello automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="66120-107">Voor meer informatie over:</span><span class="sxs-lookup"><span data-stu-id="66120-107">For more information about:</span></span>

- <span data-ttu-id="66120-108">Voorwaardelijke toegang, Zie [voorwaardelijke toegang voor Azure Active Directory op basis van apparaten](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="66120-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="66120-109">Windows 10-apparaten in Hallo werkplek en verbeterde Hallo ervaringen wanneer geregistreerd in Azure AD, Zie [Windows 10 voor ondernemingen Hallo: apparaten gebruiken voor het werk](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66120-109">Windows 10 devices in hello workplace and hello enhanced experiences when registered with Azure AD, see [Windows 10 for hello enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="66120-110">Windows 10 Enterprise E3 in CSP, Zie Hallo [Windows 10 Enterprise E3 in het overzicht van de CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="66120-110">Windows 10 Enterprise E3 in CSP, see hello [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="66120-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="66120-111">Before you begin</span></span>

<span data-ttu-id="66120-112">Voordat u begint met het configureren van Hallo automatische registratie van Windows-domein-apparaten in uw omgeving, moet u dat vertrouwd raken met de Hallo ondersteund scenario's en Hallo beperkingen.</span><span class="sxs-lookup"><span data-stu-id="66120-112">Before you start configuring hello automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="66120-113">tooimprove hello leesbaarheid Hallo beschrijvingen van Hallo na termijn maakt gebruik van dit onderwerp:</span><span class="sxs-lookup"><span data-stu-id="66120-113">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="66120-114">**Huidige Windows-apparaten** -deze term die lid zijn van toodomain apparaten met Windows 10 of Windows Server 2016 verwijst.</span><span class="sxs-lookup"><span data-stu-id="66120-114">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="66120-115">**Apparaten met Windows downlevel-** -deze term verwijst tooall **ondersteund** domein Windows-apparaten die geen actieve Windows 10 of Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="66120-115">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="66120-116">Huidige Windows-apparaten</span><span class="sxs-lookup"><span data-stu-id="66120-116">Windows current devices</span></span>

- <span data-ttu-id="66120-117">Voor apparaten met Hallo Windows desktop-besturingssysteem, wordt u aangeraden speciale Update (versie 1607) voor Windows 10 of hoger.</span><span class="sxs-lookup"><span data-stu-id="66120-117">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="66120-118">de registratie van de huidige Windows-apparaten Hallo **is** in niet-gefedereerde omgevingen zoals wachtwoord-hash-synchronisatie configuraties ondersteund.</span><span class="sxs-lookup"><span data-stu-id="66120-118">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="66120-119">Eerdere Windows-apparaten</span><span class="sxs-lookup"><span data-stu-id="66120-119">Windows down-level devices</span></span>

- <span data-ttu-id="66120-120">volgende downlevel-apparaten met Windows Hello worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="66120-120">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="66120-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="66120-121">Windows 8.1</span></span>
    - <span data-ttu-id="66120-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="66120-122">Windows 7</span></span>
    - <span data-ttu-id="66120-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="66120-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="66120-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="66120-124">Windows Server 2012</span></span>
    - <span data-ttu-id="66120-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="66120-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="66120-126">de registratie van een downlevel-apparaten met Windows Hello **is** in niet-gefedereerde omgevingen via naadloze eenmalige aanmelding ondersteund [Azure Active Directory naadloze eenmalige aanmelding](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="66120-126">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="66120-127">de registratie van een downlevel-apparaten met Windows Hello **is niet** ondersteund voor apparaten met behulp van zwervende profielen.</span><span class="sxs-lookup"><span data-stu-id="66120-127">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="66120-128">Als u gebruik van zwervende profielen of instellingen, gebruikt u Windows 10.</span><span class="sxs-lookup"><span data-stu-id="66120-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="66120-129">Vereisten</span><span class="sxs-lookup"><span data-stu-id="66120-129">Prerequisites</span></span>

<span data-ttu-id="66120-130">Voordat u begint met het inschakelen van Hallo automatische registratie van apparaten in uw organisatie lid van een domein, moet u ervoor dat u een actuele versie van Azure AD zijn uitgevoerd toomake verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="66120-130">Before you start enabling hello auto-registration of domain-joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="66120-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="66120-131">Azure AD Connect:</span></span>

- <span data-ttu-id="66120-132">Houdt Hallo-koppeling tussen het Hallo-computeraccount in uw lokale Active Directory (AD) en Hallo apparaatobject in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66120-132">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="66120-133">Andere apparaat gerelateerde functies, zoals Windows Hello voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="66120-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="66120-134">Configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="66120-134">Configuration steps</span></span>

<span data-ttu-id="66120-135">Dit onderwerp bevat stappen voor alle scenario's met standaardconfiguratie Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="66120-135">This topic includes hello required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="66120-136">Gebruik Hallo tabel tooget een overzicht van Hallo stappen die nodig voor uw scenario zijn te volgen:</span><span class="sxs-lookup"><span data-stu-id="66120-136">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="66120-137">Stappen</span><span class="sxs-lookup"><span data-stu-id="66120-137">Steps</span></span>                                      | <span data-ttu-id="66120-138">Windows huidige en het wachtwoord-hash-synchronisatie</span><span class="sxs-lookup"><span data-stu-id="66120-138">Windows current and password hash sync</span></span> | <span data-ttu-id="66120-139">De huidige Windows- en Federatie</span><span class="sxs-lookup"><span data-stu-id="66120-139">Windows current and federation</span></span> | <span data-ttu-id="66120-140">Windows downlevel-</span><span class="sxs-lookup"><span data-stu-id="66120-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="66120-141">Stap 1: Een serviceverbindingspunt configureren</span><span class="sxs-lookup"><span data-stu-id="66120-141">Step 1: Configure service connection point</span></span> | ![Selecteren][1]                            | ![Selecteren][1]                    | ![Selecteren][1]        |
| <span data-ttu-id="66120-145">Stap 2: De uitgifte van claims instellen</span><span class="sxs-lookup"><span data-stu-id="66120-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Selecteren][1]                    | ![Selecteren][1]        |
| <span data-ttu-id="66120-148">Stap 3: Windows 10-apparaten inschakelen</span><span class="sxs-lookup"><span data-stu-id="66120-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Selecteren][1]        |
| <span data-ttu-id="66120-150">Stap 4: Implementatie van het besturingselement en implementatie</span><span class="sxs-lookup"><span data-stu-id="66120-150">Step 4: Control deployment and rollout</span></span>     | ![Selecteren][1]                            | ![Selecteren][1]                    | ![Selecteren][1]        |
| <span data-ttu-id="66120-154">Stap 5: Controleren of de geregistreerde apparaten</span><span class="sxs-lookup"><span data-stu-id="66120-154">Step 5: Verify registered devices</span></span>          | ![Selecteren][1]                            | ![Selecteren][1]                    | ![Selecteren][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="66120-158">Stap 1: Een serviceverbindingspunt configureren</span><span class="sxs-lookup"><span data-stu-id="66120-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="66120-159">Hallo service connection point (SCP)-object wordt gebruikt door uw apparaten tijdens Hallo registratie toodiscover informatie over het Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="66120-159">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="66120-160">Hallo SCP-object voor Hallo automatische registratie van apparaten die lid zijn van een domein moet in uw lokale Active Directory (AD) bestaan op Hallo naming context configuratiepartitie van Hallo computerforest.</span><span class="sxs-lookup"><span data-stu-id="66120-160">In your on-premises Active Directory (AD), hello SCP object for hello auto-registration of domain-joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="66120-161">Er is slechts één configuratienaamgevingscontext per forest.</span><span class="sxs-lookup"><span data-stu-id="66120-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="66120-162">In een configuratie met meerdere forests met Active Directory moet Hallo het service connection point in alle forests met computers domein bestaan.</span><span class="sxs-lookup"><span data-stu-id="66120-162">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="66120-163">U kunt Hallo [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve Hallo configuratienaamgevingscontext van uw forest.</span><span class="sxs-lookup"><span data-stu-id="66120-163">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="66120-164">Voor een forest met Active Directory-domeinnaam Hallo *fabrikam.com*, configuratienaamgevingscontext Hallo is:</span><span class="sxs-lookup"><span data-stu-id="66120-164">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="66120-165">Hallo SCP-object voor Hallo automatische registratie van apparaten die lid zijn van een domein is in uw forest zich op:</span><span class="sxs-lookup"><span data-stu-id="66120-165">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="66120-166">Afhankelijk van hoe u Azure AD Connect hebt geïmplementeerd, Hallo SCP-object mogelijk al zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="66120-166">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="66120-167">U kunt controleren Hallo Hallo object bestaan en Hallo detectie waarden met behulp van de volgende Windows PowerShell-script Hallo ophalen:</span><span class="sxs-lookup"><span data-stu-id="66120-167">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="66120-168">Hallo **$scp. Trefwoorden** uitvoer geeft informatie weer hello Azure AD-tenant, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="66120-168">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="66120-169">Als het serviceverbindingspunt Hallo niet bestaat, kunt u dit maken door het uitvoeren van Hallo `Initialize-ADSyncDomainJoinedComputerSync` cmdlet uit op uw Azure AD Connect-server.</span><span class="sxs-lookup"><span data-stu-id="66120-169">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="66120-170">Enterprise admin credential is vereist toorun deze cmdlet.</span><span class="sxs-lookup"><span data-stu-id="66120-170">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="66120-171">Hallo-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="66120-171">hello cmdlet:</span></span>

- <span data-ttu-id="66120-172">Maakt het serviceverbindingspunt Hallo in hello Azure AD Connect is verbonden met Active Directory-forest.</span><span class="sxs-lookup"><span data-stu-id="66120-172">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="66120-173">Vereist dat u toospecify hello `AdConnectorAccount` parameter.</span><span class="sxs-lookup"><span data-stu-id="66120-173">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="66120-174">Dit is Hallo-account dat is geconfigureerd als Active Directory connector-account in Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="66120-174">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="66120-175">Hallo toont volgende script een voorbeeld voor het gebruik van Hallo-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="66120-175">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="66120-176">In dit script `$aadAdminCred = Get-Credential` moet u een gebruikersnaam tootype.</span><span class="sxs-lookup"><span data-stu-id="66120-176">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="66120-177">U moet tooprovide Hallo gebruikersnaam Hallo gebruiker UPN (User Principal Name)-indeling (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="66120-177">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="66120-178">Hallo `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="66120-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="66120-179">Maakt gebruik van de Active Directory PowerShell-module hello, die afhankelijk is van Active Directory Web Services uitgevoerd op een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="66120-179">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="66120-180">Active Directory Web Services wordt ondersteund op domeincontrollers met Windows Server 2008 R2 en hoger.</span><span class="sxs-lookup"><span data-stu-id="66120-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="66120-181">Wordt alleen ondersteund door Hallo **MSOnline PowerShell moduleversie 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="66120-181">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="66120-182">toodownload deze module gebruiken deze [koppeling](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="66120-182">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="66120-183">Voor domeincontrollers met Windows Server 2008 of eerdere versies, Hallo-script hieronder toocreate Hallo serviceverbindingspunt te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="66120-183">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="66120-184">In een configuratie met meerdere forests, moet u Hallo script toocreate Hallo het service connection point in elk forest waar computers bestaan te volgen:</span><span class="sxs-lookup"><span data-stu-id="66120-184">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="66120-185">Stap 2: De uitgifte van claims instellen</span><span class="sxs-lookup"><span data-stu-id="66120-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="66120-186">In een federatieve Azure AD-configuratie apparaten zijn afhankelijk van de Active Directory Federation Services (AD FS) of een 3e party on-premises federation service tooauthenticate tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="66120-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="66120-187">Apparaten verifiëren tooget een token tooregister toegang tegen hello Azure Active Directory Device Registration Service (DRS Azure).</span><span class="sxs-lookup"><span data-stu-id="66120-187">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="66120-188">Windows huidige apparaten met behulp van geïntegreerde Windows-verificatie tooan actieve WS-Trust eindpunt (1.3 of 2005 versies verifiëren) die worden gehost door Hallo lokale federation-service.</span><span class="sxs-lookup"><span data-stu-id="66120-188">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="66120-189">Wanneer u AD FS, ofwel **adfs/services/trust/13/windowstransport** of **adfs/services/trust/2005/windowstransport** moet zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="66120-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="66120-190">Als u Hallo webproxy verificatie gebruikt, zorg er ook voor dat dit eindpunt is gepubliceerd via Hallo proxy.</span><span class="sxs-lookup"><span data-stu-id="66120-190">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="66120-191">U kunt zien welke eindpunten worden ingeschakeld via Hallo AD FS-beheerconsole onder **Service > eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="66120-191">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="66120-192">Als u geen AD FS als de lokale federation-service, instructies Hallo van uw leverancier toomake zorgen dat ze WS-Trust 1.3 of 2005 eindpunten en deze zijn gepubliceerd via Hallo Metadata Exchange-bestand (MEX) ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="66120-192">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="66120-193">Hallo moeten volgende claims bestaan in die door Azure DRS ontvangen voor apparaat registratie toocomplete Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="66120-193">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="66120-194">Azure DRS maakt een apparaatobject in Azure AD met enkele van deze informatie die vervolgens door Azure AD Connect tooassociate Hallo nieuw apparaatobject met Hallo computer account on-premises gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="66120-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="66120-195">Als u meer dan een geverifieerde domeinnaam hebt, moet u tooprovide Hallo claim voor computers te volgen:</span><span class="sxs-lookup"><span data-stu-id="66120-195">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="66120-196">Als u al een claim onveranderbare id genoemd (bijv, alternatieve aanmeldings-ID) moet een overeenkomende claim tooprovide voor computers:</span><span class="sxs-lookup"><span data-stu-id="66120-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="66120-197">In de Hallo uit te voeren, kunt u informatie vinden over:</span><span class="sxs-lookup"><span data-stu-id="66120-197">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="66120-198">Hallo waarden elke claim moet hebben.</span><span class="sxs-lookup"><span data-stu-id="66120-198">hello values each claim should have</span></span>
- <span data-ttu-id="66120-199">Hoe een definitie eruit als in AD FS</span><span class="sxs-lookup"><span data-stu-id="66120-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="66120-200">Hallo definitie helpt u bij tooverify of Hallo waarden aanwezig zijn of als u toocreate moet ze.</span><span class="sxs-lookup"><span data-stu-id="66120-200">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="66120-201">Als u AD FS niet voor de lokale federation-server gebruikt, voert u de leverancier van uw instructies toocreate Hallo juiste configuratie tooissue deze claims.</span><span class="sxs-lookup"><span data-stu-id="66120-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="66120-202">Probleem account type claim</span><span class="sxs-lookup"><span data-stu-id="66120-202">Issue account type claim</span></span>

<span data-ttu-id="66120-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Deze claim moet een waarde van bevatten **DJ**, waarin Hallo-apparaat als een computer lid van een domein.</span><span class="sxs-lookup"><span data-stu-id="66120-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="66120-204">U kunt een regel voor het transformeren van uitgifte die uitziet toevoegen in AD FS:</span><span class="sxs-lookup"><span data-stu-id="66120-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="66120-205">Probleem objectGUID van Hallo computer account lokale</span><span class="sxs-lookup"><span data-stu-id="66120-205">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="66120-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Deze claim Hallo moet bevatten **objectGUID** waarde Hallo lokale computeraccount.</span><span class="sxs-lookup"><span data-stu-id="66120-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="66120-207">U kunt een regel voor het transformeren van uitgifte die uitziet toevoegen in AD FS:</span><span class="sxs-lookup"><span data-stu-id="66120-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="66120-208">Probleem objectSID van Hallo computer account lokale</span><span class="sxs-lookup"><span data-stu-id="66120-208">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="66120-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Deze claim Hallo Hallo moet bevatten **objectSid** waarde Hallo lokale computeraccount.</span><span class="sxs-lookup"><span data-stu-id="66120-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="66120-210">U kunt een regel voor het transformeren van uitgifte die uitziet toevoegen in AD FS:</span><span class="sxs-lookup"><span data-stu-id="66120-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="66120-211">IssuerID voor computer uitgeven wanneer meerdere domeinnamen in Azure AD geverifieerd</span><span class="sxs-lookup"><span data-stu-id="66120-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="66120-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Deze claim moet Hallo id URI (Uniform Resource) van een Hallo geverifieerd domeinnamen die verbinding maken met de Hallo lokale federation-service (AD FS of 3e partij) verlenende Hallo token bevatten.</span><span class="sxs-lookup"><span data-stu-id="66120-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="66120-213">U kunt in AD FS uitgifte transformatieregels die eruitzien zoals toepassingsgroepen onderstaande Hallo in die specifieke volgorde na Hallo toepassingsgroepen bovenstaande toevoegen.</span><span class="sxs-lookup"><span data-stu-id="66120-213">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="66120-214">Houd er rekening mee dat één regel tooexplicitly probleem Hallo-regel voor gebruikers nodig is.</span><span class="sxs-lookup"><span data-stu-id="66120-214">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="66120-215">In onderstaande Hallo regels, wordt een eerste regel voor het identificeren van gebruiker versus computerverificatie toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="66120-215">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with hello value User when its not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
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


<span data-ttu-id="66120-216">In bovenstaande Hallo-claim</span><span class="sxs-lookup"><span data-stu-id="66120-216">In hello claim above,</span></span>

- <span data-ttu-id="66120-217">`$<domain>`Hallo AD FS-service-URL is</span><span class="sxs-lookup"><span data-stu-id="66120-217">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="66120-218">`<verified-domain-name>`is een tijdelijke aanduiding moet u tooreplace met een van uw geverifieerde domeinnamen in Azure AD</span><span class="sxs-lookup"><span data-stu-id="66120-218">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="66120-219">Zie voor meer informatie over geverifieerde domeinnamen [toevoegen van een aangepast domein naam tooAzure Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="66120-219">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="66120-220">een lijst van uw bedrijf geverifieerde domeinen tooget, kunt u Hallo [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="66120-220">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="66120-222">Onveranderbare id genoemd uitgeven voor computer, als een voor gebruikers bestaat (bijvoorbeeld alternatieve aanmeldings-ID is ingesteld)</span><span class="sxs-lookup"><span data-stu-id="66120-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="66120-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**-Deze claim moet een geldige waarde voor computers bevatten.</span><span class="sxs-lookup"><span data-stu-id="66120-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="66120-224">In AD FS, kunt u een regel voor het transformeren van uitgifte als volgt:</span><span class="sxs-lookup"><span data-stu-id="66120-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="66120-225">Helper toocreate Hallo AD FS uitgifte transformatie scriptregels</span><span class="sxs-lookup"><span data-stu-id="66120-225">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="66120-226">Hallo kunt volgende script u met Hallo maken van Hallo uitgifte transformeren regels die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="66120-226">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

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
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
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

### <a name="remarks"></a><span data-ttu-id="66120-227">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="66120-227">Remarks</span></span> 

- <span data-ttu-id="66120-228">Dit script wordt Hallo regels toohello bestaande regels toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="66120-228">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="66120-229">Hallo-script worden niet uitgevoerd tweemaal omdat Hallo reeks regels zou twee keer worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="66120-229">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="66120-230">Zorg ervoor dat er geen overeenkomende regels bestaan voor deze claims (onder de bijbehorende voorwaarden Hallo) voordat Hallo script nogmaals uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="66120-230">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="66120-231">Als u meerdere geverifieerde domeinnamen hebben (zoals weergegeven in hello Azure AD-portal of via de cmdlet Get-MsolDomains Hallo), stelt u de waarde Hallo van **$multipleVerifiedDomainNames** in Hallo script te**$true**.</span><span class="sxs-lookup"><span data-stu-id="66120-231">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="66120-232">Controleer ook of u een bestaande issuerid claim die mogelijk zijn gemaakt met Azure AD Connect of via andere middelen.</span><span class="sxs-lookup"><span data-stu-id="66120-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="66120-233">Hier volgt een voorbeeld voor deze regel:</span><span class="sxs-lookup"><span data-stu-id="66120-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="66120-234">Als u al uitgegeven een **onveranderbare id genoemd** claim voor gebruikersaccounts, stelt u Hallo-waarde van **$immutableIDAlreadyIssuedforUsers** in Hallo script te**$true**.</span><span class="sxs-lookup"><span data-stu-id="66120-234">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="66120-235">Stap 3: Eerdere Windows-apparaten inschakelen</span><span class="sxs-lookup"><span data-stu-id="66120-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="66120-236">Als sommige van uw apparaten domein Windows downlevel-apparaten, moet u naar:</span><span class="sxs-lookup"><span data-stu-id="66120-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="66120-237">Een beleid in Azure AD-tooenable tooregister apparaten van gebruikers instellen.</span><span class="sxs-lookup"><span data-stu-id="66120-237">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="66120-238">Configureren van de lokale federation-service tooissue claims toosupport **geïntegreerde Windows-verificatie (IWA)** voor apparaatregistratie.</span><span class="sxs-lookup"><span data-stu-id="66120-238">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="66120-239">Hello Azure AD apparaat verificatie eindpunt toohello lokale intranetzones tooavoid certificaat vraagt bij het verifiëren van Hallo apparaat toevoegen.</span><span class="sxs-lookup"><span data-stu-id="66120-239">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="66120-240">Beleid instellen in Azure AD-tooenable tooregister apparaten van gebruikers</span><span class="sxs-lookup"><span data-stu-id="66120-240">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="66120-241">tooregister Windows downlevel-apparaten, moet u ervoor dat gebruikers tooallow tooregister apparaten instellen in Azure AD hello wordt ingesteld toomake.</span><span class="sxs-lookup"><span data-stu-id="66120-241">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="66120-242">In hello Azure-portal, kunt u deze instelling onder vinden:</span><span class="sxs-lookup"><span data-stu-id="66120-242">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="66120-243">Hallo volgende beleid moet worden ingesteld te**alle**: **gebruikers hun apparaten kunnen registreren met Azure AD**</span><span class="sxs-lookup"><span data-stu-id="66120-243">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Apparaten registreren](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="66120-245">Configureren van de lokale federation-service</span><span class="sxs-lookup"><span data-stu-id="66120-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="66120-246">De lokale federation-service moet ondersteunen verlenende Hallo **authenticationmehod** en **wiaormultiauthn** claims tijdens het ontvangen van een verificatie aanvragen toohello Azure AD relying party die een resouce_params parameter met een gecodeerde waarde zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="66120-246">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="66120-247">Wanneer een dergelijke aanvraag afkomstig is, Hallo lokale federation-service Hallo-gebruiker met behulp van geïntegreerde Windows-verificatie moet worden geverifieerd en dit lukt, moet het Hallo na twee claims uitgeven:</span><span class="sxs-lookup"><span data-stu-id="66120-247">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="66120-248">In AD FS, moet u een regel voor het transformeren van uitgifte die verificatiemethode geeft via Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="66120-248">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="66120-249">**tooadd met deze regel:**</span><span class="sxs-lookup"><span data-stu-id="66120-249">**tooadd this rule:**</span></span>

1. <span data-ttu-id="66120-250">Ga te in Hallo AD FS-beheerconsole`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="66120-250">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="66120-251">Hallo Identiteitsplatform van Microsoft Office 365 relying party trust-object met de rechtermuisknop en selecteer vervolgens **Claimregels bewerken**.</span><span class="sxs-lookup"><span data-stu-id="66120-251">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="66120-252">Op Hallo **uitgifte Transformatieregels** tabblad **regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="66120-252">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="66120-253">In Hallo **claimregel** lijst met sjablonen, selecteer **Claims verzenden met een aangepaste regel**.</span><span class="sxs-lookup"><span data-stu-id="66120-253">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="66120-254">Selecteer **volgende**.</span><span class="sxs-lookup"><span data-stu-id="66120-254">Select **Next**.</span></span>
6. <span data-ttu-id="66120-255">In Hallo **naam Claimregel** in het vak **Auth methode Claimregel**.</span><span class="sxs-lookup"><span data-stu-id="66120-255">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="66120-256">In Hallo **claimregel** vak, type Hallo-regel:</span><span class="sxs-lookup"><span data-stu-id="66120-256">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="66120-257">Typ op de federatieserver Hallo PowerShell-opdracht hieronder na het vervangen  **\<RPObjectName\>**  met Hallo relying party objectnaam voor uw Azure AD relying party trust-object.</span><span class="sxs-lookup"><span data-stu-id="66120-257">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="66120-258">Dit object meestal heet **Identiteitsplatform van Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="66120-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="66120-259">Hello Azure AD apparaat verificatie eindpunt toohello Lokaal Intranet zones toevoegen</span><span class="sxs-lookup"><span data-stu-id="66120-259">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="66120-260">tooavoid certificaat wordt gevraagd wanneer gebruikers in het register apparaten verifiëren tooAzure AD kunt u een beleid tooyour domeinapparaten tooadd Hallo URL-zone toohello Lokaal Intranet in Internet Explorer na pushen:</span><span class="sxs-lookup"><span data-stu-id="66120-260">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="66120-261">Stap 4: Implementatie van het besturingselement en implementatie</span><span class="sxs-lookup"><span data-stu-id="66120-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="66120-262">Wanneer u Hallo vereiste stappen hebt voltooid, worden apparaten die lid zijn van een domein gereed tooautomatically registreren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66120-262">When you have completed hello required steps, domain-joined devices are ready tooautomatically register with Azure AD.</span></span> <span data-ttu-id="66120-263">Alle domein op apparaten met Windows 10 Verjaardag Update en Windows Server 2016 automatisch registreren met Azure AD op het apparaat opnieuw wordt gestart of gebruikersaanmelding.</span><span class="sxs-lookup"><span data-stu-id="66120-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="66120-264">Nieuwe apparaten registreren met Azure AD wanneer Hallo-apparaat opnieuw wordt gestart nadat Hallo domain join-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="66120-264">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

<span data-ttu-id="66120-265">Apparaten die eerder met de werkplek zijn toegevoegd tooAzure AD (bijvoorbeeld voor Intune) overgang te zijn'*lid van een domein, geregistreerd bij AAD*"; maar het duurt even totdat dit proces toocomplete op alle apparaten vanwege toohello normaal de stroom van de domein- en gebruikersactiviteit.</span><span class="sxs-lookup"><span data-stu-id="66120-265">Devices that were previously workplace-joined tooAzure AD (for example for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="66120-266">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="66120-266">Remarks</span></span>

- <span data-ttu-id="66120-267">U kunt een Group Policy object toocontrol Hallo rollout van automatische inschrijving van Windows 10 en Windows Server 2016 domein computers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="66120-267">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="66120-268">Windows 10 November 2015 automatisch bijwerken registers met Azure AD **alleen** als Hallo implementatie Groepsbeleid-object is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="66120-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="66120-269">toorollout hello automatische registratie van Windows downlevel-computers, u kunt een [Windows Installer-pakket](#windows-installer-packages-for-non-windows-10-computers) toocomputers die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="66120-269">toorollout hello automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="66120-270">Als u push-Hallo Group Policy object tooWindows 8.1 domein apparaten, worden registratie geprobeerd; maar het wordt aangeraden dat u Hallo [Windows Installer-pakket](#windows-installer-packages-for-non-windows-10-computers) tooregister al uw Windows downlevel-apparaten.</span><span class="sxs-lookup"><span data-stu-id="66120-270">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) tooregister all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="66120-271">Een groepsbeleidsobject maken</span><span class="sxs-lookup"><span data-stu-id="66120-271">Create a Group Policy object</span></span> 

<span data-ttu-id="66120-272">toocontrol hello rollout van automatische registratie van de huidige Windows-computers, moet u Hallo implementeren **Domeincomputers registreren als apparaten** Group Policy object toohello apparaten gewenste tooregister.</span><span class="sxs-lookup"><span data-stu-id="66120-272">toocontrol hello rollout of automatic registration of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="66120-273">U kunt bijvoorbeeld Hallo beleid tooan organisatie-eenheid of beveiligingsgroep tooa implementeren.</span><span class="sxs-lookup"><span data-stu-id="66120-273">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="66120-274">**tooset hello beleid:**</span><span class="sxs-lookup"><span data-stu-id="66120-274">**tooset hello policy:**</span></span>

1. <span data-ttu-id="66120-275">Open **Serverbeheer**, en ga te`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="66120-275">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="66120-276">Ga naar toohello domeinknooppunt dat overeenkomt met toohello domein waarvoor u tooactivate automatische registratie van de huidige Windows-computers.</span><span class="sxs-lookup"><span data-stu-id="66120-276">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="66120-277">Met de rechtermuisknop op **Group Policy Objects**, en selecteer vervolgens **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="66120-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="66120-278">Typ een naam voor uw groepsbeleidsobject.</span><span class="sxs-lookup"><span data-stu-id="66120-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="66120-279">Bijvoorbeeld: *automatische registratie tooAzure AD*.</span><span class="sxs-lookup"><span data-stu-id="66120-279">For example, *Automatic Registration tooAzure AD*.</span></span> <span data-ttu-id="66120-280">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="66120-280">Select **OK**.</span></span>
5. <span data-ttu-id="66120-281">Met de rechtermuisknop op uw nieuwe groepsbeleidsobject en selecteer vervolgens **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="66120-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="66120-282">Ga te**Computerconfiguratie** > **beleid** > **Beheersjablonen** > **Windows Onderdelen** > **apparaatregistratie**.</span><span class="sxs-lookup"><span data-stu-id="66120-282">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="66120-283">Met de rechtermuisknop op **Domeincomputers registreren als apparaten**, en selecteer vervolgens **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="66120-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="66120-284">Deze groepsbeleidssjabloon gewijzigd van eerdere versies van de console Groepsbeleidsbeheer Hallo.</span><span class="sxs-lookup"><span data-stu-id="66120-284">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="66120-285">Als u een eerdere versie van het Hallo-console gebruikt, gaat u verder te`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="66120-285">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="66120-286">Selecteer **ingeschakeld**, en selecteer vervolgens **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="66120-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="66120-287">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="66120-287">Select **OK**.</span></span>
9. <span data-ttu-id="66120-288">Koppeling hello Group Policy object tooa locatie van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="66120-288">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="66120-289">Bijvoorbeeld, kunt u deze koppelen tooa specifieke organisatie-eenheid.</span><span class="sxs-lookup"><span data-stu-id="66120-289">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="66120-290">Ook kan koppelt u het tooa beveiligingsgroep met computers die automatisch wordt geregistreerd bij Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66120-290">You also could link it tooa specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="66120-291">tooset dit beleid voor alle Windows 10 en Windows Server 2016 Domeincomputers in uw organisatie, koppeling Hallo Group Policy object toohello domein.</span><span class="sxs-lookup"><span data-stu-id="66120-291">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="66120-292">Windows Installer-pakketten voor Windows 10-computers</span><span class="sxs-lookup"><span data-stu-id="66120-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="66120-293">tooregister domein Windows downlevel-computers in een federatieve omgeving, kunt u downloaden en installeren van deze Windows Installer-pakket (.msi) van Downloadcentrum op Hallo [Microsoft Workplace Join voor Windows 10-computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) pagina.</span><span class="sxs-lookup"><span data-stu-id="66120-293">tooregister domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="66120-294">U kunt Hallo pakket implementeren met behulp van een software-distributiesysteem zoals System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="66120-294">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="66120-295">Hallo pakket ondersteunt Hallo standaard stille installatieopties Hello *stille* parameter.</span><span class="sxs-lookup"><span data-stu-id="66120-295">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="66120-296">System Center Configuration Manager Current Branch biedt extra voordelen van eerdere versies, zoals Hallo mogelijkheid tootrack voltooid registraties.</span><span class="sxs-lookup"><span data-stu-id="66120-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="66120-297">Zie voor meer informatie [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="66120-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="66120-298">Hallo-installatieprogramma maakt een geplande taak op Hallo-systeem die wordt uitgevoerd in de context van de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="66120-298">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="66120-299">Hallo-taak wordt geactiveerd wanneer Hallo gebruiker zich aanmeldt tooWindows.</span><span class="sxs-lookup"><span data-stu-id="66120-299">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="66120-300">Hallo taak registreert achtergrond Hallo-apparaat met Azure AD met gebruikersreferenties Hallo na verificatie met behulp van geïntegreerde Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="66120-300">hello task silently registers hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="66120-301">toosee hello geplande taak in het Hallo-apparaat, gaat u te**Microsoft** > **Workplace Join**, en ga toohello Task Scheduler-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="66120-301">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="66120-302">Stap 5: Controleren of de geregistreerde apparaten</span><span class="sxs-lookup"><span data-stu-id="66120-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="66120-303">U kunt geslaagde geregistreerde apparaten in uw organisatie controleren met behulp van Hallo [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in Hallo [Azure Active Directory PowerShell-module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="66120-303">You can check successful registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="66120-304">Hallo-uitvoer van deze cmdlet toont de apparaten die zijn geregistreerd bij Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66120-304">hello output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="66120-305">tooget alle apparaten gebruiken Hallo **-alle** parameter en filter ze met behulp van Hallo **deviceTrustType** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="66120-305">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="66120-306">Verbonden met het domein apparaten hebben een waarde van **domein**.</span><span class="sxs-lookup"><span data-stu-id="66120-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66120-307">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="66120-307">Next steps</span></span>

* [<span data-ttu-id="66120-308">Automatische apparaatregistratie Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="66120-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="66120-309">Automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD – Windows 10 en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="66120-309">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="66120-310">Automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD – Windows 10</span><span class="sxs-lookup"><span data-stu-id="66120-310">Troubleshooting auto-registration of domain joined computers tooAzure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="66120-311">Voorwaardelijke toegang van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66120-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png

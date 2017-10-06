---
title: aaaSilent toepassingsproxy van Azure AD-connector installeren | Microsoft Docs
description: Bevat informatie over hoe een installatie zonder toezicht van Azure AD-Application Proxy Connector tooprovide veilige externe toegang tooyour tooperform lokale apps.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3aa1c7f2-fb2a-4693-abd5-95bb53700cbb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ce796ff45a65ba7d5f0f63c02085bdc6af494548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="d62ee-103">Achtergrond hello Azure AD-Application Proxy Connector te installeren</span><span class="sxs-lookup"><span data-stu-id="d62ee-103">Silently install hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="d62ee-104">Wilt u toobe kunnen toosend installatie van een script toomultiple Windows-servers of tooWindows-Servers waarvoor geen gebruikersinterface is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d62ee-104">You want toobe able toosend an installation script toomultiple Windows servers or tooWindows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="d62ee-105">Dit onderwerp helpt u bij het maken van een Windows PowerShell-script waarmee de installatie zonder toezicht en registratie voor uw Azure AD Application Proxy Connector.</span><span class="sxs-lookup"><span data-stu-id="d62ee-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="d62ee-106">Deze mogelijkheid is handig als u wilt:</span><span class="sxs-lookup"><span data-stu-id="d62ee-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="d62ee-107">Hallo-connector installeren op computers zonder gebruikersinterface-laag, of wanneer u RDP toohello machine niet.</span><span class="sxs-lookup"><span data-stu-id="d62ee-107">Install hello connector on machines with no UI layer or when you cannot RDP toohello machine.</span></span>
* <span data-ttu-id="d62ee-108">Installeren en veel connectors in één keer te registreren.</span><span class="sxs-lookup"><span data-stu-id="d62ee-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="d62ee-109">Hallo-connector installeren en registreren als onderdeel van een andere procedure integreren.</span><span class="sxs-lookup"><span data-stu-id="d62ee-109">Integrate hello connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="d62ee-110">Maakt een standaard serverinstallatiekopie die bevat Hallo connector bits, maar is niet geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="d62ee-110">Create a standard server image that contains hello connector bits but is not registered.</span></span>

<span data-ttu-id="d62ee-111">Toepassingsproxy werkt door een dunne Windows Server-service aangeroepen Hallo Connector in uw netwerk te installeren.</span><span class="sxs-lookup"><span data-stu-id="d62ee-111">Application Proxy works by installing a slim Windows Server service called hello Connector inside your network.</span></span> <span data-ttu-id="d62ee-112">Hallo Connector voor toepassingsproxy toowork heeft toobe geregistreerd bij uw Azure AD-directory met een globale beheerder en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d62ee-112">For hello Application Proxy Connector toowork it has toobe registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="d62ee-113">Deze informatie wordt normaal gesproken ingevoerd tijdens de installatie van de Connector in een pop-updialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d62ee-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="d62ee-114">Echter, kunt u Windows PowerShell toocreate een referentie-object tooenter uw registratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="d62ee-114">However, you can use Windows PowerShell toocreate a credential object tooenter your registration information.</span></span> <span data-ttu-id="d62ee-115">Of u kunt uw eigen token maken en gebruiken deze tooenter uw registratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="d62ee-115">Or you can create your own token and use it tooenter your registration information.</span></span>

## <a name="install-hello-connector"></a><span data-ttu-id="d62ee-116">Hallo-connector installeren</span><span class="sxs-lookup"><span data-stu-id="d62ee-116">Install hello connector</span></span>
<span data-ttu-id="d62ee-117">Hallo Connector MSI-bestanden installeren zonder te registreren Hallo Connector als volgt:</span><span class="sxs-lookup"><span data-stu-id="d62ee-117">Install hello Connector MSIs without registering hello Connector as follows:</span></span>

1. <span data-ttu-id="d62ee-118">Open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="d62ee-118">Open a command prompt.</span></span>
2. <span data-ttu-id="d62ee-119">Uitvoeren van de volgende opdracht in welke Hallo /q stille installatie betekent Hallo - hello installatie niet wordt gevraagd u tooaccept Hallo gebruiksrechtovereenkomst.</span><span class="sxs-lookup"><span data-stu-id="d62ee-119">Run hello following command in which hello /q means quiet installation - hello installation doesn't prompt you tooaccept hello End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a><span data-ttu-id="d62ee-120">Hallo connector registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="d62ee-120">Register hello connector with Azure AD</span></span>
<span data-ttu-id="d62ee-121">Er zijn twee methoden kunt u tooregister Hallo-connector:</span><span class="sxs-lookup"><span data-stu-id="d62ee-121">There are two methods you can use tooregister hello connector:</span></span>

* <span data-ttu-id="d62ee-122">Hallo-connector met behulp van een Windows PowerShell-referentieobject registreren</span><span class="sxs-lookup"><span data-stu-id="d62ee-122">Register hello connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="d62ee-123">Registreren van een token gemaakt offline Hallo-connector</span><span class="sxs-lookup"><span data-stu-id="d62ee-123">Register hello connector using a token created offline</span></span>

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="d62ee-124">Hallo-connector met behulp van een Windows PowerShell-referentieobject registreren</span><span class="sxs-lookup"><span data-stu-id="d62ee-124">Register hello connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="d62ee-125">Hallo Windows PowerShell-referenties object maken door deze opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d62ee-125">Create hello Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="d62ee-126">Vervang  *\<gebruikersnaam\>*  en  *\<wachtwoord\>*  met Hallo gebruikersnaam en wachtwoord voor uw directory:</span><span class="sxs-lookup"><span data-stu-id="d62ee-126">Replace *\<username\>* and *\<password\>* with hello username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="d62ee-127">Ga te**C:\Program Files\Microsoft AAD App Proxy Connector** en Voer Hallo script met behulp van PowerShell Hallo referenties object u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d62ee-127">Go too**C:\Program Files\Microsoft AAD App Proxy Connector** and run hello script using hello PowerShell credentials object you created.</span></span> <span data-ttu-id="d62ee-128">Vervang *$cred* met de naam van de Hallo Hallo PowerShell referenties object u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="d62ee-128">Replace *$cred* with hello name of hello PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a><span data-ttu-id="d62ee-129">Registreren van een token gemaakt offline Hallo-connector</span><span class="sxs-lookup"><span data-stu-id="d62ee-129">Register hello connector using a token created offline</span></span>
1. <span data-ttu-id="d62ee-130">Maken van een offline-token Hallo AuthenticationContext klasse via Hallo waarden in het codefragment hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d62ee-130">Create an offline token using hello AuthenticationContext class using hello values in hello code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// hello AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// hello application ID of hello connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// hello reply address of hello connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// hello AppIdUri of hello registration service in AAD
        /// </summary>
        static readonly Uri RegistrationServiceAppIdUri = new Uri("https://proxy.cloudwebappproxy.net/registerapp");

        #endregion

        #region private members
        private string token;
        private string tenantID;
        #endregion

        public void GetAuthenticationToken()
        {
            AuthenticationContext authContext = new AuthenticationContext(AadAuthenticationEndpoint.AbsoluteUri);

            AuthenticationResult authResult = authContext.AcquireToken(RegistrationServiceAppIdUri.AbsoluteUri,
                ConnectorAppId,
                ConnectorRedirectAddress,
                PromptBehavior.Always);

            if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
            {
                Trace.TraceError("Authentication result, token or tenant id returned are null");
                throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
            }

            token = authResult.AccessToken;
            tenantID = authResult.TenantId;
        }


2. <span data-ttu-id="d62ee-131">Zodra u Hallo-token hebt, maakt u een token gebruikt Hallo SecureString:</span><span class="sxs-lookup"><span data-stu-id="d62ee-131">Once you have hello token, create a SecureString using hello token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="d62ee-132">Voer Hallo Windows PowerShell-opdracht te volgen en vervangt \<tenant-GUID\> aan uw directory-ID:</span><span class="sxs-lookup"><span data-stu-id="d62ee-132">Run hello following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="d62ee-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d62ee-133">Next steps</span></span> 
* [<span data-ttu-id="d62ee-134">Toepassingen publiceren met uw eigen domeinnaam</span><span class="sxs-lookup"><span data-stu-id="d62ee-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="d62ee-135">Eenmalige aanmelding inschakelen</span><span class="sxs-lookup"><span data-stu-id="d62ee-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="d62ee-136">Oplossen van problemen met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="d62ee-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)



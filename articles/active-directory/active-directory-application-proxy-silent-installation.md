---
title: Een installatie zonder toezicht toepassingsproxy van Azure AD-connector | Microsoft Docs
description: Bevat informatie over het uitvoeren van een installatie zonder toezicht van Azure AD Connector voor toepassingsproxy om te bieden veilige externe toegang tot uw lokale apps.
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
ms.openlocfilehash: 9e28c89d8f64f0ae3d4150017ca544e606075c45
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="silently-install-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="0337c-103">De Azure AD Application Proxy Connector achtergrond te installeren</span><span class="sxs-lookup"><span data-stu-id="0337c-103">Silently install the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="0337c-104">U wilt dat een script voor installatie verzenden naar meerdere Windows-servers of Windows-Servers waarvoor geen gebruikersinterface is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0337c-104">You want to be able to send an installation script to multiple Windows servers or to Windows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="0337c-105">Dit onderwerp helpt u bij het maken van een Windows PowerShell-script waarmee de installatie zonder toezicht en registratie voor uw Azure AD Application Proxy Connector.</span><span class="sxs-lookup"><span data-stu-id="0337c-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="0337c-106">Deze mogelijkheid is handig als u wilt:</span><span class="sxs-lookup"><span data-stu-id="0337c-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="0337c-107">De connector installeren op computers zonder gebruikersinterface-laag, of wanneer u RDP kan niet aan de machine.</span><span class="sxs-lookup"><span data-stu-id="0337c-107">Install the connector on machines with no UI layer or when you cannot RDP to the machine.</span></span>
* <span data-ttu-id="0337c-108">Installeren en veel connectors in één keer te registreren.</span><span class="sxs-lookup"><span data-stu-id="0337c-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="0337c-109">De installatie van connector en de registratie als onderdeel van een andere procedure integreren.</span><span class="sxs-lookup"><span data-stu-id="0337c-109">Integrate the connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="0337c-110">Maak een Standard van SQL server-installatiekopie die de connector bits bevat maar is niet geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="0337c-110">Create a standard server image that contains the connector bits but is not registered.</span></span>

<span data-ttu-id="0337c-111">Toepassingsproxy werkt door een dunne Windows Server-service aangeroepen van de Connector in uw netwerk te installeren.</span><span class="sxs-lookup"><span data-stu-id="0337c-111">Application Proxy works by installing a slim Windows Server service called the Connector inside your network.</span></span> <span data-ttu-id="0337c-112">Heeft voor de Connector voor toepassingsproxy werkt deze worden geregistreerd met uw Azure AD-directory met een globale beheerder en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="0337c-112">For the Application Proxy Connector to work it has to be registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="0337c-113">Deze informatie wordt normaal gesproken ingevoerd tijdens de installatie van de Connector in een pop-updialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0337c-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="0337c-114">Echter, kunt u Windows PowerShell voor het maken van een referentieobject uw registratie-informatie in te voeren.</span><span class="sxs-lookup"><span data-stu-id="0337c-114">However, you can use Windows PowerShell to create a credential object to enter your registration information.</span></span> <span data-ttu-id="0337c-115">Of u kunt uw eigen token maken en gebruiken deze gegevens voor de productregistratie invoeren.</span><span class="sxs-lookup"><span data-stu-id="0337c-115">Or you can create your own token and use it to enter your registration information.</span></span>

## <a name="install-the-connector"></a><span data-ttu-id="0337c-116">De connector installeren</span><span class="sxs-lookup"><span data-stu-id="0337c-116">Install the connector</span></span>
<span data-ttu-id="0337c-117">Het MSI-bestanden voor de Connector installeren zonder te registreren van de Connector als volgt:</span><span class="sxs-lookup"><span data-stu-id="0337c-117">Install the Connector MSIs without registering the Connector as follows:</span></span>

1. <span data-ttu-id="0337c-118">Open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="0337c-118">Open a command prompt.</span></span>
2. <span data-ttu-id="0337c-119">Voer de volgende opdracht die de /q stille installatie - betekent dat de installatie niet wordt gevraagd u accepteert de gebruiksrechtovereenkomst.</span><span class="sxs-lookup"><span data-stu-id="0337c-119">Run the following command in which the /q means quiet installation - the installation doesn't prompt you to accept the End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-the-connector-with-azure-ad"></a><span data-ttu-id="0337c-120">Registreert u de connector met Azure AD</span><span class="sxs-lookup"><span data-stu-id="0337c-120">Register the connector with Azure AD</span></span>
<span data-ttu-id="0337c-121">Er zijn twee methoden die kunt u de connector te registreren:</span><span class="sxs-lookup"><span data-stu-id="0337c-121">There are two methods you can use to register the connector:</span></span>

* <span data-ttu-id="0337c-122">De connector met behulp van een Windows PowerShell-referentieobject registreren</span><span class="sxs-lookup"><span data-stu-id="0337c-122">Register the connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="0337c-123">Registreert u de connector met behulp van een token offline gemaakt</span><span class="sxs-lookup"><span data-stu-id="0337c-123">Register the connector using a token created offline</span></span>

### <a name="register-the-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="0337c-124">De connector met behulp van een Windows PowerShell-referentieobject registreren</span><span class="sxs-lookup"><span data-stu-id="0337c-124">Register the connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="0337c-125">De Windows PowerShell-referenties-object maken door deze opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="0337c-125">Create the Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="0337c-126">Vervang  *\<gebruikersnaam\>*  en  *\<wachtwoord\>*  met de gebruikersnaam en wachtwoord voor uw directory:</span><span class="sxs-lookup"><span data-stu-id="0337c-126">Replace *\<username\>* and *\<password\>* with the username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="0337c-127">Ga naar **C:\Program Files\Microsoft AAD App Proxy Connector** en voer het script met de PowerShell referenties object u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0337c-127">Go to **C:\Program Files\Microsoft AAD App Proxy Connector** and run the script using the PowerShell credentials object you created.</span></span> <span data-ttu-id="0337c-128">Vervang *$cred* met de naam van de PowerShell-referenties object u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="0337c-128">Replace *$cred* with the name of the PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-the-connector-using-a-token-created-offline"></a><span data-ttu-id="0337c-129">Registreert u de connector met behulp van een token offline gemaakt</span><span class="sxs-lookup"><span data-stu-id="0337c-129">Register the connector using a token created offline</span></span>
1. <span data-ttu-id="0337c-130">Maken van een offline-token met behulp van de AuthenticationContext klasse met de waarden in het codefragment:</span><span class="sxs-lookup"><span data-stu-id="0337c-130">Create an offline token using the AuthenticationContext class using the values in the code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// The AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// The application ID of the connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// The reply address of the connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// The AppIdUri of the registration service in AAD
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


2. <span data-ttu-id="0337c-131">Zodra u het token hebt, maakt u een SecureString met behulp van het token:</span><span class="sxs-lookup"><span data-stu-id="0337c-131">Once you have the token, create a SecureString using the token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="0337c-132">Voer de volgende Windows PowerShell-opdracht vervangen \<tenant-GUID\> aan uw directory-ID:</span><span class="sxs-lookup"><span data-stu-id="0337c-132">Run the following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="0337c-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0337c-133">Next steps</span></span> 
* [<span data-ttu-id="0337c-134">Toepassingen publiceren met uw eigen domeinnaam</span><span class="sxs-lookup"><span data-stu-id="0337c-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="0337c-135">Eenmalige aanmelding inschakelen</span><span class="sxs-lookup"><span data-stu-id="0337c-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="0337c-136">Oplossen van problemen met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="0337c-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)



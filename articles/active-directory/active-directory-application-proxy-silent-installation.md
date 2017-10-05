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
# <a name="silently-install-the-azure-ad-application-proxy-connector"></a>De Azure AD Application Proxy Connector achtergrond te installeren
U wilt dat een script voor installatie verzenden naar meerdere Windows-servers of Windows-Servers waarvoor geen gebruikersinterface is ingeschakeld. Dit onderwerp helpt u bij het maken van een Windows PowerShell-script waarmee de installatie zonder toezicht en registratie voor uw Azure AD Application Proxy Connector.

Deze mogelijkheid is handig als u wilt:

* De connector installeren op computers zonder gebruikersinterface-laag, of wanneer u RDP kan niet aan de machine.
* Installeren en veel connectors in één keer te registreren.
* De installatie van connector en de registratie als onderdeel van een andere procedure integreren.
* Maak een Standard van SQL server-installatiekopie die de connector bits bevat maar is niet geregistreerd.

Toepassingsproxy werkt door een dunne Windows Server-service aangeroepen van de Connector in uw netwerk te installeren. Heeft voor de Connector voor toepassingsproxy werkt deze worden geregistreerd met uw Azure AD-directory met een globale beheerder en het wachtwoord. Deze informatie wordt normaal gesproken ingevoerd tijdens de installatie van de Connector in een pop-updialoogvenster. Echter, kunt u Windows PowerShell voor het maken van een referentieobject uw registratie-informatie in te voeren. Of u kunt uw eigen token maken en gebruiken deze gegevens voor de productregistratie invoeren.

## <a name="install-the-connector"></a>De connector installeren
Het MSI-bestanden voor de Connector installeren zonder te registreren van de Connector als volgt:

1. Open een opdrachtprompt.
2. Voer de volgende opdracht die de /q stille installatie - betekent dat de installatie niet wordt gevraagd u accepteert de gebruiksrechtovereenkomst.
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-the-connector-with-azure-ad"></a>Registreert u de connector met Azure AD
Er zijn twee methoden die kunt u de connector te registreren:

* De connector met behulp van een Windows PowerShell-referentieobject registreren
* Registreert u de connector met behulp van een token offline gemaakt

### <a name="register-the-connector-using-a-windows-powershell-credential-object"></a>De connector met behulp van een Windows PowerShell-referentieobject registreren
1. De Windows PowerShell-referenties-object maken door deze opdracht uit te voeren. Vervang  *\<gebruikersnaam\>*  en  *\<wachtwoord\>*  met de gebruikersnaam en wachtwoord voor uw directory:
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. Ga naar **C:\Program Files\Microsoft AAD App Proxy Connector** en voer het script met de PowerShell referenties object u hebt gemaakt. Vervang *$cred* met de naam van de PowerShell-referenties object u hebt gemaakt:
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-the-connector-using-a-token-created-offline"></a>Registreert u de connector met behulp van een token offline gemaakt
1. Maken van een offline-token met behulp van de AuthenticationContext klasse met de waarden in het codefragment:

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


2. Zodra u het token hebt, maakt u een SecureString met behulp van het token:

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. Voer de volgende Windows PowerShell-opdracht vervangen \<tenant-GUID\> aan uw directory-ID:

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a>Volgende stappen 
* [Toepassingen publiceren met uw eigen domeinnaam](active-directory-application-proxy-custom-domains.md)
* [Eenmalige aanmelding inschakelen](active-directory-application-proxy-sso-using-kcd.md)
* [Oplossen van problemen met toepassingsproxy](active-directory-application-proxy-troubleshoot.md)



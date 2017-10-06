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
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a>Achtergrond hello Azure AD-Application Proxy Connector te installeren
Wilt u toobe kunnen toosend installatie van een script toomultiple Windows-servers of tooWindows-Servers waarvoor geen gebruikersinterface is ingeschakeld. Dit onderwerp helpt u bij het maken van een Windows PowerShell-script waarmee de installatie zonder toezicht en registratie voor uw Azure AD Application Proxy Connector.

Deze mogelijkheid is handig als u wilt:

* Hallo-connector installeren op computers zonder gebruikersinterface-laag, of wanneer u RDP toohello machine niet.
* Installeren en veel connectors in één keer te registreren.
* Hallo-connector installeren en registreren als onderdeel van een andere procedure integreren.
* Maakt een standaard serverinstallatiekopie die bevat Hallo connector bits, maar is niet geregistreerd.

Toepassingsproxy werkt door een dunne Windows Server-service aangeroepen Hallo Connector in uw netwerk te installeren. Hallo Connector voor toepassingsproxy toowork heeft toobe geregistreerd bij uw Azure AD-directory met een globale beheerder en het wachtwoord. Deze informatie wordt normaal gesproken ingevoerd tijdens de installatie van de Connector in een pop-updialoogvenster. Echter, kunt u Windows PowerShell toocreate een referentie-object tooenter uw registratie-informatie. Of u kunt uw eigen token maken en gebruiken deze tooenter uw registratie-informatie.

## <a name="install-hello-connector"></a>Hallo-connector installeren
Hallo Connector MSI-bestanden installeren zonder te registreren Hallo Connector als volgt:

1. Open een opdrachtprompt.
2. Uitvoeren van de volgende opdracht in welke Hallo /q stille installatie betekent Hallo - hello installatie niet wordt gevraagd u tooaccept Hallo gebruiksrechtovereenkomst.
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a>Hallo connector registreren met Azure AD
Er zijn twee methoden kunt u tooregister Hallo-connector:

* Hallo-connector met behulp van een Windows PowerShell-referentieobject registreren
* Registreren van een token gemaakt offline Hallo-connector

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a>Hallo-connector met behulp van een Windows PowerShell-referentieobject registreren
1. Hallo Windows PowerShell-referenties object maken door deze opdracht uit te voeren. Vervang  *\<gebruikersnaam\>*  en  *\<wachtwoord\>*  met Hallo gebruikersnaam en wachtwoord voor uw directory:
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. Ga te**C:\Program Files\Microsoft AAD App Proxy Connector** en Voer Hallo script met behulp van PowerShell Hallo referenties object u hebt gemaakt. Vervang *$cred* met de naam van de Hallo Hallo PowerShell referenties object u hebt gemaakt:
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a>Registreren van een token gemaakt offline Hallo-connector
1. Maken van een offline-token Hallo AuthenticationContext klasse via Hallo waarden in het codefragment hello gebruiken:

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


2. Zodra u Hallo-token hebt, maakt u een token gebruikt Hallo SecureString:

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. Voer Hallo Windows PowerShell-opdracht te volgen en vervangt \<tenant-GUID\> aan uw directory-ID:

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a>Volgende stappen 
* [Toepassingen publiceren met uw eigen domeinnaam](active-directory-application-proxy-custom-domains.md)
* [Eenmalige aanmelding inschakelen](active-directory-application-proxy-sso-using-kcd.md)
* [Oplossen van problemen met toepassingsproxy](active-directory-application-proxy-troubleshoot.md)



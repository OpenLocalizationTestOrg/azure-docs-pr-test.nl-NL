---
title: aaaAzure AD-federatiecompatibiliteitslijst
description: Deze pagina is niet-Microsoft id-providers die gebruikt tooimplement worden kunnen eenmalige aanmelding.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 22c8693e-8915-446d-b383-27e9587988ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: ac2f9ad324c8ca6b587b73ea465426ad6b074b03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-federation-compatibility-list"></a>Azure AD-federation compatibiliteitslijst
Azure Active Directory biedt eenmalige aanmelding op en verbeterde beveiliging van toepassingen toegang voor Office 365 en andere Microsoft Online services voor hybride en alleen in de cloud-implementaties zonder een niet-Microsoft-oplossing. Office 365, zoals de meeste van de Microsoft Online services, is geïntegreerd met Azure Active Directory voor adreslijstservices, verificatie en autorisatie. Azure Active Directory biedt ook eenmalige aanmelding toothousands van SaaS-toepassingen en lokale webtoepassingen. Zie hello Azure Active Directory-toepassingsgalerie voor ondersteunde SaaS-toepassingen.

Voor organisaties die hebben geïnvesteerd in niet-Microsoft-federatieoplossingen, bevat dit onderwerp instructies voor het configureren van eenmalige aanmelding voor de Windows Server Active Directory-gebruikers met Microsoft Online services met behulp van niet-Microsoft-id-providers van Hallo 'Azure Active Directory federatiecompatibiliteitslijst' hieronder. 

![](./media/active-directory-aadconnect-federation-compatibility/oxford2.jpg)   
[Computergroep Oxford](http://oxfordcomputergroup.com/), een derde getest namens Microsoft, deze eenmalige aanmelding met niet-Microsoft-identiteitsproviders op basis van een verzameling van algemene gebruiksvoorbeelden met Azure Active Directory.

Voor informatie over hoe u hier vermeld van derden id-provider kan krijgen, neem contact op met de computergroep Oxford op [ idp@oxfordcomputergroup.com ](mailto:idp@oxfordcomputergroup.com).

> [!IMPORTANT]
> Computergroep Oxford getest alleen Hallo federation functionaliteit van deze scenario voor eenmalige aanmelding. Computergroep Oxford heeft geen uitgevoerd voor alle tests van Hallo synchronisatie, tweeledige verificatie, enzovoort onderdelen van deze scenario voor eenmalige aanmelding.
> 
> Gebruik van de aanmelding door alternatieve ID tooUPN is ook niet getest in dit programma.
> 
> 

* [Azure Active Directory](#azure-active-directory)
* [AuthAnvil eenmalige aanmelding 4.5](#authanvil-single-sign-on-45)
* [BIG-IP-adres met beleidsbeheer toegang BIG-IP-versie 11, lid 3 x – 11, 6 x](#big-ip-with-access-policy-manager-big-ip-ver-113x--116x) 
* [BitGlass](#bitglass)
* [Beveiligde CA-Cloud](#ca-secure-cloud) 
* [CA-SiteMinder 12.52](#ca-siteminder-1252-sp1-cumulative-release-4) 
* [Centrify](#centrify) 
* [Dell één identiteitsbeheer Cloud toegang v7.1](#dell-one-identity-cloud-access-manager-v71) 
* [DigitalPersona samengestelde verificatie](#digitalpersona-composite-authentication)
* [IBM Tivoli federatieve Identity Manager 6.2.2](#ibm-tivoli-federated-identity-manager-622) 
* [IceWall Federation versie 3.0](#icewall-federation-version-30) 
* [Memority](#memority)
* [NetIQ Access Manager 4.x](#netiq-access-manager-4x) 
* [Okta](#okta) 
* [OneLogin](#onelogin) 
* [Optimale IDM identiteit van virtuele Server Federatieservices](#optimal-idm-virtual-identity-server-federation-services) 
* [PingFederate 6.11, 7.2, 8.x](#pingfederate-611-72-8x)
* [RadiantOne CFS 3.0](#radiantone-cfs-30) 
* [Sailpoint IdentityNow](#sailpoint-identitynow)
* [SecureAuth IdP 7.2.0](#secureauth-idp-720) 
* [Meld u aan & 5.3 start](#signgo-53) 
* [SoftBank technologie Online Service-Gate](#softbank)
* [VMware-werkruimte een](#vmware-workspace-one)



> [!IMPORTANT]
> Aangezien deze producten van derden, biedt Microsoft geen ondersteuning voor Hallo implementatie, configuratie, probleemoplossing, best practices, enz. problemen en vragen met betrekking tot deze id-providers. Voor ondersteuning en vragen met betrekking tot deze id-providers rechtstreeks contact opnemen met derden Hallo ondersteund.
> 
> Deze derde partij identiteitsproviders zijn getest op compatibiliteit met Microsoft cloudservices met behulp van WS-Federation en alleen de WS-Trust-protocollen. Testen bevat geen met Hallo SAML-protocol.
> 


## <a name="azure-active-directory"></a>Azure Active Directory

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding: 

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geen |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geen |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |
| Moderne toepassingen die gebruikmaken van ADAL zoals Office 2016 |Ondersteund |Geen |

Zie voor meer informatie over het gebruik van Azure Active Directory met AD FS [Active Directory Federation Services (ADFS)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).

Zie voor meer informatie over het gebruik van Azure Active Directory met Password sync [Azure AD Connect](active-directory-aadconnect.md).

## <a name="authanvil-single-sign-on-45"></a>AuthAnvil eenmalige aanmelding 4.5

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie [AuthAnvil eenmalige aanmelding.](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-).


## <a name="big-ip-with-access-policy-manager-big-ip-ver-113x--116x"></a>BIG-IP-adres met beleidsbeheer toegang BIG-IP-versie 11, lid 3 x – 11, 6 x

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding: 

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geen |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Niet ondersteund |Niet ondersteund |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over BIG-IP Access Policy Manager [beleidsbeheer BIG-IP-toegang.](https://f5.com/products/modules/access-policy-manager) 

Hallo voor Hallo BIG-IP Access Policy Manager instructies over hoe tooconfigure deze STS tooprovide Hallo ervaring voor eenmalige aanmelding tooyour Active Directory: gebruikers downloaden pdf [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf).

## <a name="bitglass"></a>BitGlass

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over BitGlass [BitGlass](http://www.bitglass.com).

## <a name="ca-secure-cloud"></a>Beveiligde CA-Cloud

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over CA Secure Cloud [CA Secure Cloud](http://www.ca.com/us/products/security-as-a-service.aspx).

## <a name="ca-siteminder-1252-sp1-cumulative-release-4"></a>CA SiteMinder 12.52 SP1 cumulatieve versie 4

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding: 

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geen |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geen |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over CA SiteMinder [CA SiteMinder Federation](http://www.ca.com/us/products/ca-single-sign-on.html). 

## <a name="centrify"></a>Centrify

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geen |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geen |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Client-toegangsbeheer wordt niet ondersteund. |

Zie voor meer informatie over Centrify [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp).

## <a name="dell-one-identity-cloud-access-manager-v71"></a>Dell één identiteitsbeheer Cloud toegang v7.1

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geen |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geen |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over Dell één identiteit Cloud Access Manager [Dell één Cloud toegang identiteitsbeheer](http://software.dell.com/products/cloud-access-manager).

 Voor Hallo instructies over hoe tooconfigure deze STS tooprovide Hallo ervaring voor eenmalige aanmelding tooyour Office 365-gebruikers zien [Office 365-gebruikers configureren](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365). 

## <a name="digitalpersona-composite-authentication"></a>DigitalPersona samengestelde verificatie  

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund.|
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund.|
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie [DigitalPersona samengestelde verificatie](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf).


## <a name="ibm-tivoli-federated-identity-manager-622"></a>IBM Tivoli federatieve Identity Manager 6.2.2

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding: 

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geen |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geen |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over IBM Tivoli federatieve Identity Manager [IBM Security toegang Manager for Microsoft Applications](http://www-01.ibm.com/support/docview.wss?uid=swg24029517).

## <a name="icewall-federation-version-30"></a>IceWall Federation versie 3.0

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over IceWall Federation [IceWall Federation versie 3.0](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/) en [IceWall Federatie met Office 365](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html).

## <a name="memority"></a>Memority

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding: 

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geen |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geen |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over het gebruik van Memority [Memority](http://www.memority.com).


## <a name="netiq-access-manager-4x"></a>NetIQ Access Manager 4.x

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geen|
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geen|
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie [NetIQ Access Manager](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m).

## <a name="okta"></a>Okta

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding: 

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geïntegreerde Windows-verificatie is vereist voor installatie van extra webserver en Okta-toepassing. |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geïntegreerde Windows-verificatie |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over Okta [Okta](https://www.okta.com/).

## <a name="onelogin"></a>OneLogin

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding: 

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geïntegreerde Windows-verificatie |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geïntegreerde Windows-verificatie |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over OneLogin [OneLogin](https://www.onelogin.com/).

## <a name="optimal-idm-virtual-identity-server-federation-services"></a>Optimale IDM identiteit van virtuele Server Federatieservices

Hallo volgende Hallo scenario ondersteuningsmatrix-deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geen |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geïntegreerde Windows-verificatie |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |

Voor meer informatie over client toegangsbeleid Zie [toegang beperken tooOffice 365 Services op basis van locatie van de Client Hallo Hallo](https://technet.microsoft.com/library/hh526961.aspx).





## <a name="pingfederate-611-72-8x"></a>PingFederate 6.11, 7.2, 8.x

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geen |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geen |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Voor Hallo PingFederate instructies over hoe tooconfigure deze STS tooprovide Hallo eenmalige aanmelding optreden Zie tooyour Active Directory-gebruikers, een van de volgende Hallo: 

- [PingFederate 6.11](http://go.microsoft.com/fwlink/?LinkID=266321)
- [7.2 PingFederate](http://documentation.pingidentity.com/display/PF72/PingFederate+7.2)
- [PingFederate 8.x](http://documentation.pingidentity.com/display/PFS/SSO+to+Office+365+Introduction)

## <a name="radiantone-cfs-30"></a>RadiantOne CFS 3.0

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding: 

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geen |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geïntegreerde Windows-verificatie |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over RadiantOne CFS [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/).

## <a name="sailpoint-identitynow"></a>Sailpoint IdentityNow

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/).

## <a name="secureauth-idp-720"></a>SecureAuth IdP 7.2.0

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding: 

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geen |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geen |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over SecureAuth [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293).














## <a name="signgo-53"></a>Meld u aan & 5.3 start

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Kerberos-contracten ondersteund |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geen |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Aanmelding & Ga 5.3 biedt ondersteuning voor Kerberos-verificatie via configuratie van een Kerberos-Contract.  Neem voor hulp bij deze configuratie kunt contact op met Ilex of weergave Hallo installatiehandleiding [aanmelding & Ga](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)

## <a name="softbank-technology-online-service-gate"></a>SoftBank technologie Online Service-Gate

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over SoftBank technologie Online Service-Gate [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)

## <a name="vmware-workspace-one"></a>VMware-werkruimte een

Hallo volgt Hallo scenario ondersteuningsmatrix voor deze ervaring voor eenmalige aanmelding:

| Client | Ondersteuning | Uitzonderingen |
| --- | --- | --- |
| Web-gebaseerde clients zoals Exchange Web Access en SharePoint Online |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| Interactieve toepassingen zoals Lync, Office-abonnement, CRM |Ondersteund |Geïntegreerde Windows-verificatie wordt niet ondersteund. |
| E-rich clients, zoals Outlook en ActiveSync |Ondersteund |Geen |

Zie voor meer informatie over [VMware werkruimte één](http://www.vmware.com/pdf/vidm-office365-saml.pdf)


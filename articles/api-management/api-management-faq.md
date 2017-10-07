---
title: aaaAzure Veelgestelde vragen over de API Management | Microsoft Docs
description: Meer informatie over Hallo beantwoordt toocommon vragen, patronen en aanbevolen procedures in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 9e7cdf1b881a4dfed4bd2cfd7fbb4994f48b5f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-faqs"></a>Azure API Management-Veelgestelde vragen
Hallo-antwoorden toocommon vragen, patronen en aanbevolen procedures voor Azure API Management worden opgehaald.

## <a name="contact-us"></a>Contact opnemen
* [Hoe kan ik vraag het team van Microsoft Azure API Management Hallo?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>Veelgestelde vragen
* [Wat betekent het als een functie in preview?](#what-does-it-mean-when-a-feature-is-in-preview)
* [Hoe kan ik Hallo verbinding tussen Hallo API Management-gateway en Mijn back-end-services beveiligen?](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [Hoe kopieer ik mijn service-exemplaar tooa nieuw exemplaar van API Management?](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [Kan ik mijn exemplaar van API Management programmatisch beheren?](#can-i-manage-my-api-management-instance-programmatically)
* [Hoe kan ik een gebruikersgroep toohello-beheerders toevoegen](#how-do-i-add-a-user-to-the-administrators-group)
* [Waarom is dat ik wil tooadd niet beschikbaar in de beleidseditor Hallo Hallo-beleid?](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [Hoe gebruik API-versies in API Management?](#how-do-i-use-api-versioning-in-api-management)
* [Hoe stel ik omgevingen met meerdere in één API](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [Kan ik SOAP gebruiken met API Management?](#can-i-use-soap-with-api-management)
* [Hallo API Management gateway-IP-adres constante is? Kan ik deze in firewallregels gebruiken?](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [Kan ik een OAuth 2.0-autorisatie-server configureren met AD FS-beveiliging?](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [Welke methode voor het doorsturen gebruikt API Management in implementaties toomultiple geografische locaties?](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [Kan ik een Azure Resource Manager-sjabloon toocreate exemplaar van API Management-service gebruiken?](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [Kan ik een zelf-ondertekend SSL-certificaat gebruiken voor een back-end](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [Waarom krijg ik een verificatiefout opgetreden wanneer ik probeer tooclone een GIT-opslagplaats?](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [Werkt API Management met Azure ExpressRoute?](#does-api-management-work-with-azure-expressroute)
* [Waarom hebben we een specifieke subnet in het Resource Manager-stijl VNETs nodig wanneer API Management wordt geïmplementeerd in deze?](#why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them)
* [Wat is de minimale subnetgrootte Hallo nodig bij het implementeren van API Management in een VNET?](#what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet)
* [Kan ik een API Management-service van een abonnement tooanother verplaatsen?](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [Zijn er beperkingen op of bekende problemen met mijn API importeren?](#are-there-restrictions-on-or-known-issues-with-importing-my-api)

### <a name="how-can-i-ask-hello-microsoft-azure-api-management-team-a-question"></a>Hoe kan ik vraag het team van Microsoft Azure API Management Hallo?
U kunt contact met ons opnemen via een van de volgende opties:

* Stel uw vragen in onze [API Management MSDN-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt).
* E-mailbericht te verzenden<mailto:apimgmt@microsoft.com>.
* Stuur ons een functie-aanvraag in Hallo [Azure Feedbackforum](https://feedback.azure.com/forums/248703-api-management).

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>Wat betekent het als een functie in preview?
Wanneer een functie in preview is, betekent dit dat we op zoek bent actief naar feedback over hoe Hallo functie voor u werkt. Er is een functie in preview functioneel voltooid, maar het is mogelijk dat maken we een recente wijziging in het antwoord toocustomer feedback. Het is raadzaam dat u niet afhankelijk zijn van een functie die in het voorbeeld in uw productieomgeving. Als u feedback op de preview-functies hebt, laat ons weten via een Hallo Contactopties in [hoe kan ik Microsoft Azure API Management-team Hallo Stel een vraag?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question).

### <a name="how-can-i-secure-hello-connection-between-hello-api-management-gateway-and-my-back-end-services"></a>Hoe kan ik Hallo verbinding tussen Hallo API Management-gateway en Mijn back-end-services beveiligen?
U hebt verschillende opties toosecure Hallo verbinding tussen Hallo API Management-gateway en de back-end-services. U kunt:

* Gebruik HTTP-basisverificatie. Zie voor meer informatie [instellingen voor de API configureren](api-management-howto-create-apis.md#configure-api-settings).
* Gebruik van wederzijdse verificatie van SSL, zoals beschreven in [hoe toosecure back-end-services met behulp van verificatie van clientcertificaten in Azure API Management](api-management-howto-mutual-certificates.md).
* IP-whitelisting op uw back-end-service gebruiken. Als u een standaard of Premium-laag API Management-exemplaar hebt, Hallo IP-adres van gateway Hallo constant is gebleven. U kunt uw tooallow geaccepteerde dit IP-adres instellen. U krijgt Hallo IP-adres van uw API Management-exemplaar op Hallo Dashboard in hello Azure-portal.
* Verbinding maken met uw API Management-exemplaar tooan Azure Virtual Network.

### <a name="how-do-i-copy-my-api-management-service-instance-tooa-new-instance"></a>Hoe kopieer ik mijn service-exemplaar tooa nieuw exemplaar van API Management?
Als u wilt dat een nieuw exemplaar van API Management-exemplaar tooa toocopy hebt u verschillende mogelijkheden. U kunt:

* Gebruik Hallo back-up en herstel van de functie in API Management. Zie voor meer informatie [hoe tooimplement noodherstel met behulp van service-back-up en herstel in Azure API Management](api-management-howto-disaster-recovery-backup-restore.md).
* Uw eigen back-up maken en terugzetten van de functie met Hallo [API Management REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx). Gebruik Hallo REST-API toosave en Hallo entiteiten van Hallo service-exemplaar dat u wilt herstellen.
* Hallo-serviceconfiguratie downloaden met behulp van Git en upload het tooa nieuw exemplaar. Zie voor meer informatie [hoe toosave en de configuratie van uw API Management-service configureren met behulp van Git](api-management-configuration-repository-git.md).

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>Kan ik mijn exemplaar van API Management programmatisch beheren?
Ja, kunt u API Management programmatisch beheren door gebruik te maken:

* Hallo [API Management REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx).
* Hallo [Microsoft Azure ApiManagement Service Management-bibliotheek SDK](http://aka.ms/apimsdk).
* Hallo [implementatie](https://msdn.microsoft.com/library/mt619282.aspx) en [servicebeheer](https://msdn.microsoft.com/library/mt613507.aspx) PowerShell-cmdlets.

### <a name="how-do-i-add-a-user-toohello-administrators-group"></a>Hoe kan ik een gebruikersgroep toohello-beheerders toevoegen
Hier ziet u hoe u een gebruikersgroep voor toohello beheerders kunt toevoegen:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Ga toohello resourcegroep die Hallo gewenste tooupdate API Management-exemplaar heeft.
3. Wijs in API Management Hallo **Api Management Inzender** rol toohello gebruiker.

Nu Hallo toegevoegde Inzender kunt Azure PowerShell gebruiken [cmdlets](https://msdn.microsoft.com/library/mt613507.aspx). Hier ziet u hoe toosign in als beheerder:

1. Gebruik Hallo `Login-AzureRmAccount` cmdlet toosign in.
2. Stel Hallo context toohello-abonnement met Hallo service met behulp van `Set-AzureRmContext -SubscriptionID <subscriptionGUID>`.
3. Ophalen van een URL met eenmalige aanmelding met behulp van `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>`.
4. Hallo URL tooaccess Hallo-beheerportal gebruiken.

### <a name="why-is-hello-policy-that-i-want-tooadd-unavailable-in-hello-policy-editor"></a>Waarom is dat ik wil tooadd niet beschikbaar in de beleidseditor Hallo Hallo-beleid?
Als Hallo-beleid dat u wilt dat tooadd wordt weergegeven grijs of grijs in de beleidseditor hello weergegeven, moet u dat u zich in het juiste bereik Hallo voor Hallo-beleid. Elke instructie beleid is bedoeld voor toouse specifieke bereiken en beleid-secties. Zie informatie over het gebruik van het beleid Hallo tooreview Hallo beleid secties en bereiken voor een beleid sectie [API Management-beleidsregels](https://msdn.microsoft.com/library/azure/dn894080.aspx).

### <a name="how-do-i-use-api-versioning-in-api-management"></a>Hoe gebruik API-versies in API Management?
U hebt een aantal opties toouse API-versies in API Management:

* U kunt verschillende versies van API's toorepresent configureren in API Management. Bijvoorbeeld, wellicht u twee verschillende API's, MyAPIv1 en MyAPIv2. Een ontwikkelaar kunt Hallo-versie die ontwikkelaars Hallo wil toouse.
* U kunt ook uw API configureren met een service-URL die een versiesegment, bijvoorbeeld https://my.api niet opgenomen. Configureer vervolgens een versiesegment op van elke bewerking [herschrijven van URL](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL) sjabloon. U kunt bijvoorbeeld een bewerking met een [URL sjabloon](api-management-howto-add-operations.md#url-template) /resource aangeroepen en een [herschrijven van URL](api-management-howto-add-operations.md#rewrite-url-template) sjabloon aangeroepen/v1/Resource. Hallo versiewaarde segment afzonderlijk voor elke bewerking, kunt u wijzigen.
* Als u tookeep wilt een segment 'standaard' versie in Hallo van API-service-URL, op geselecteerde bewerkingen een beleid instellen dat gebruikmaakt van Hallo [back-endservice ingesteld](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService) beleid toochange Hallo back-end-Aanvraagpad.

### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>Hoe stel ik omgevingen met meerdere in één API
tooset meerdere omgevingen, bijvoorbeeld een testomgeving en een productie-omgeving in één API, hebt u twee opties. U kunt:

* Host verschillende API's op Hallo dezelfde tenant.
* Host Hallo dezelfde API's op verschillende tenants.

### <a name="can-i-use-soap-with-api-management"></a>Kan ik SOAP gebruiken met API Management?
[SOAP-pass-through](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/) ondersteuning is nu beschikbaar. Beheerders kunnen importeren Hallo WSDL van de SOAP-service en Azure API Management maakt een SOAP-front-end. Portal-documentatie voor ontwikkelaars, test-console, beleid en analytics zijn allemaal beschikbaar voor de SOAP-services.

### <a name="is-hello-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>Hallo API Management gateway-IP-adres constante is? Kan ik deze in firewallregels gebruiken?
Hallo Standard en Premium lagen is Hallo openbare IP-adres (VIP) van Hallo API Management-tenant statisch voor Hallo levensduur van de tenant hello, met enkele uitzonderingen. Hallo IP-adreswijzigingen in deze omstandigheden:

* Hallo-service is verwijderd en opnieuw gemaakt.
* Hallo-serviceabonnement is [onderbroken](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) of [gewaarschuwd](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) (bijvoorbeeld voor nonpayment) en vervolgens opnieuw ingesteld.
* U toevoegen of verwijderen van Azure Virtual Network (u kunt virtueel netwerk gebruiken alleen op Hallo Developer- en Premium-laag).

Voor implementaties met meerdere landen/regio, Hallo regionale adreswijzigingen als Hallo regio wordt leeggemaakt en vervolgens opnieuw ingesteld (u kunt meerdere landen/regio-implementatie alleen op Hallo Premium-laag).

Premium-laag tenants die zijn geconfigureerd voor de implementatie van meerdere landen/regio kan één openbaar IP-adres per regio zijn toegewezen.

U kunt uw IP-adres (of de adressen in een implementatie met meerdere landen/regio) ophalen op Hallo tenant pagina in hello Azure-portal.

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>Kan ik een OAuth 2.0-autorisatie-server configureren met AD FS-beveiliging?
hoe tooconfigure een OAuth 2.0-autorisatie-server met Active Directory Federation Services (AD FS)-beveiliging, Zie toolearn [met behulp van AD FS in API Management](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/).

### <a name="what-routing-method-does-api-management-use-in-deployments-toomultiple-geographic-locations"></a>Welke methode voor het doorsturen gebruikt API Management in implementaties toomultiple geografische locaties?
API Management maakt gebruik van Hallo [prestaties methode voor het doorsturen van verkeer](../traffic-manager/traffic-manager-routing-methods.md#priority) in implementaties toomultiple geografische locaties. Binnenkomend verkeer wordt gerouteerd toohello dichtstbijzijnde API-gateway. Als één regio offline gaat, wordt binnenkomend verkeer automatisch gerouteerde toohello volgende dichtstbijzijnde gateway. Meer informatie over methoden voor het doorsturen in [methoden voor het doorsturen van Traffic Manager](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="can-i-use-an-azure-resource-manager-template-toocreate-an-api-management-service-instance"></a>Kan ik een Azure Resource Manager-sjabloon toocreate exemplaar van API Management-service gebruiken?
Ja. Zie Hallo [Azure API Management-Service](http://aka.ms/apimtemplate) Quick Start-sjablonen.

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>Kan ik een zelf-ondertekend SSL-certificaat gebruiken voor een back-end
Ja. Hier ziet u hoe toouse een zelf-ondertekend Secure Sockets Layer (SSL) van het certificaat voor een back-end:

1. Maak een [back-end](https://msdn.microsoft.com/library/azure/dn935030.aspx) entiteit met behulp van API Management.
2. Set Hallo **skipCertificateChainValidation** eigenschap te**true**.
3. Als u niet langer tooallow zelfondertekende certificaten wilt, Hallo back-end entiteit verwijderen of stel Hallo **skipCertificateChainValidation** eigenschap te**false**.

### <a name="why-do-i-get-an-authentication-failure-when-i-try-tooclone-a-git-repository"></a>Waarom krijg ik een verificatiefout opgetreden wanneer ik probeer tooclone een Git-opslagplaats?
Als u Git Referentiebeheer gebruiken of als u probeert een Git-opslagplaats tooclone met behulp van Visual Studio, kunt u een bekend probleem met het dialoogvenster Windows-referenties Hallo kunt tegenkomen. dialoogvenster Hallo beperkt wachtwoordlengte too127 tekens en het Hallo Microsoft gegenereerd wachtwoord afgekapt. We werken aan het Hallo wachtwoord verkorten. Op dit moment gebruik Git Bash tooclone de Git-opslagplaats.

### <a name="does-api-management-work-with-azure-expressroute"></a>Werkt API Management met Azure ExpressRoute?
Ja. API Management werkt met Azure ExpressRoute.

### <a name="why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them"></a>Waarom hebben we een specifieke subnet in het Resource Manager-stijl VNETs nodig wanneer API Management wordt geïmplementeerd in deze?
Hallo toegewezen subnet vereiste voor API Management zijn afkomstig van Hallo feit, dat deze is gebaseerd op (PAAS-V1-laag) klassieke implementatiemodel. We kunnen implementeren in een Resource Manager VNET (V2 layer), maar er zijn gevolgen toothat. Hallo klassieke implementatiemodel in Azure is niet nauw samen met de Hallo Resource Manager-model en kan dus als u een resource in V2-laag maakt, Hallo V1 laag niet kent het en problemen kunnen optreden, zoals API Management toouse probeert een IP-adres dat al is toegewezen tooa NIC (gebaseerd op V2).
meer informatie over het verschil tussen het klassieke en het Resource Manager-modellen in Azure te verwijzen toolearn[verschil in implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md).

### <a name="what-is-hello-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet"></a>Wat is de minimale subnetgrootte Hallo nodig bij het implementeren van API Management in een VNET?
de minimale grootte Hallo nodig toodeploy API Management is [/29](../virtual-network/virtual-networks-faq.md#configuration), namelijk Hallo minimale subnetgrootte die ondersteuning biedt voor Azure.

### <a name="can-i-move-an-api-management-service-from-one-subscription-tooanother"></a>Kan ik een API Management-service van een abonnement tooanother verplaatsen?
Ja. toolearn Zie [verplaatsen van resources tooa nieuwe resourcegroep of abonnement](../azure-resource-manager/resource-group-move-resources.md).

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>Zijn er beperkingen op of bekende problemen met mijn API importeren?
[Bekende problemen en beperkingen](api-management-api-import-restrictions.md) voor Open API(Swagger) WSDL en WADL indelingen.

---
title: aaaConfiguring een Web Application Firewall (WAF) voor App Service-omgeving
description: Meer informatie over hoe een webtoepassing tooconfigure firewall voor uw App Service-omgeving.
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>Web Application Firewall (WAF) configureren voor App Service-omgeving
## <a name="overview"></a>Overzicht
Web application firewalls zoals Hallo [Barracuda WAF voor Azure](https://www.barracuda.com/programs/azure) die beschikbaar is op Hallo [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helpt uw webtoepassingen beveiligen door web binnenkomend verkeer tooblock SQL te bekijken injectie, Cross-Site Scripting, malware uploads & DDoS-toepassing en andere aanvallen. Deze ook inspecteert Hallo-antwoorden van back-end-webservers Hallo gegevens gegevensverlies te voorkomen (DLP). In combinatie met de Hallo isolatie en aanvullende schalen geleverd door App Service-omgevingen, biedt dit een ideale omgeving toohost business kritieke webtoepassingen die toowithstand schadelijke aanvragen en grote hoeveelheden verkeer nodig.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>Instellen
Onze App Service-omgeving achter meerdere load balanced exemplaren van Barracuda WAF voor dit document die we configureert zodat alleen verkeer van Hallo WAF Hallo App Service-omgeving bereiken kan en zal deze niet toegankelijk is vanaf Hallo DMZ. We ook hebt Azure Traffic Manager voor onze Barracuda WAF exemplaren tooload saldo in Azure-datacenters en regio's. Een hoog niveau diagram van Hallo setup eruit zou wat wordt hieronder weergegeven.

![Architectuur][Architecture] 

> Opmerking: met de introductie van Hallo [ILB ondersteuning voor App Service-omgeving](app-service-environment-with-internal-load-balancer.md), kunt u configureren Hallo as-omgeving toobe niet toegankelijk vanuit Hallo DMZ en worden alleen beschikbaar toohello particuliere netwerk. 
> 
> 

## <a name="configuring-your-app-service-environment"></a>Uw App-serviceomgeving configureren
een App-serviceomgeving tooconfigure te verwijzen[onze documentatie](app-service-web-how-to-create-an-app-service-environment.md) op Hallo onderwerp. Zodra u een App-serviceomgeving is gemaakt hebt, kunt u [Web-Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) en [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in deze omgeving die al worden beveiligd achter Hallo WAF we in de volgende sectie Hallo configureren.

## <a name="configuring-your-barracuda-waf-cloud-service"></a>Uw Barracuda WAF Cloud Service configureren
Barracuda heeft een [gedetailleerde artikel](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) over het implementeren van de WAF op een virtuele machine in Azure. Maar omdat we redundantie wilt en geen een potentieel risico introduceren, u ten minste 2 toodeploy WAF exemplaar virtuele machines in Hallo dezelfde Cloud-Service wanneer deze instructies te volgen.

### <a name="adding-endpoints-toocloud-service"></a>Toevoegen van eindpunten tooCloud Service
Nadat u 2 hebt of meer WAF VM-in uw Cloud-Service exemplaren kunt u Hallo [Azure-portal](https://portal.azure.com/) tooadd HTTP en HTTPS-eindpunten die worden gebruikt door uw toepassing, zoals wordt weergegeven in onderstaande afbeelding voor Hallo.

![-Eindpunt configureren][ConfigureEndpoint]

Als uw toepassingen met andere eindpunten, moet u ervoor dat tooadd die toothis lijst met. 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>Barracuda WAF via de beheerportal configureren
Barracuda WAF maakt gebruik van TCP-poort 8000 voor configuratie via de beheerportal. Omdat er meerdere exemplaren van virtuele machines Hallo-WAF moet u hier toorepeat Hallo stappen voor elke VM-instantie. 

> Opmerking: Wanneer u klaar bent met WAF configuratie verwijderd Hallo TCP/8000 endpoint van alle virtuele machines WAF-tookeep uw beveiligde WAF.
> 
> 

Hallo management eindpunt zoals weergegeven in de afbeelding hieronder tooconfigure Hallo uw Barracuda WAF toevoegen.

![Management-eindpunt toevoegen][AddManagementEndpoint]

Gebruik een browser toobrowse toohello management-eindpunt op uw Cloud-Service. Als uw Cloudservice test.cloudapp.net aangeroepen wordt, zou u dit eindpunt openen door te bladeren toohttp://test.cloudapp.net:8000. U ziet een aanmeldingspagina zoals hieronder dat u zich kunt aanmelden met referenties die u hebt opgegeven in VM-installatiefase Hallo WAF.

![Aanmeldingspagina voor beheer][ManagementLoginPage]

Eenmaal u aanmelding ziet u een dashboard als Hallo in de afbeelding hieronder die Hallo biedt elementaire statistieken over Hallo WAF beveiliging.

![Management Dashboard][ManagementDashboard]

Te klikken op het tabblad Hallo-Services kunt u uw WAF voor services die deze beveiligt configureren. U kunt raadplegen voor meer informatie over het configureren van uw WAF Barracuda [hun documentatie](https://techlib.barracuda.com/waf/getstarted1). In voorbeeld Hallo hieronder een Azure-Web-App is voor verkeer op HTTP- en HTTPS geconfigureerd.

![Management-Services toevoegen][ManagementAddServices]

> Opmerking: Afhankelijk van hoe uw toepassingen worden geconfigureerd en welke functies worden gebruikt in uw App Service-omgeving, moet u tooforward verkeer voor TCP-poorten dan 80 en 443, bijvoorbeeld als u setup voor IP-SSL voor een Web-App. Voor een lijst met netwerkpoorten die in App Service-omgevingen worden gebruikt, raadpleegt u te[inkomend verkeer voor beheer-documentatie](app-service-app-service-environment-control-inbound-traffic.md) netwerkpoorten sectie.
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>Configureren van Microsoft Azure Traffic Manager (optioneel)
Als uw toepassing beschikbaar in meerdere regio's is, moet u tooload saldo zou willen ze achter [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). toodo zodat u een eindpunt in Hallo toevoegen kunt [klassieke Azure-portal](https://manage.azure.com) Hallo Cloud Service-naam voor uw WAF in Hallo Traffic Manager-profiel gebruiken, zoals in Hallo in onderstaande afbeelding. 

![Traffic Manager-eindpunt][TrafficManagerEndpoint]

Als uw toepassing verificatie vereist, zorg ervoor dat u hebt een resource die geen verificatie voor het Traffic Manager tooping voor beschikbaarheid van uw toepassing hello vereist. U kunt URL onder sectie configureren Hallo Hallo configureren op Hallo [klassieke Azure-portal](https://manage.azure.com) zoals hieronder wordt weergegeven.

![Traffic Manager configureren][ConfigureTrafficManager]

tooforward hello Traffic Manager-pings van uw WAF tooyour toepassing, moet u vertalingen toosetup Website op uw Barracuda WAF tooforward verkeer tooyour toepassing zoals weergegeven in Hallo voorbeeld hieronder.

![Vertalingen van de website][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a>Beveiliging van verkeer tooApp Service omgeving met behulp van Netwerkbeveiligingsgroep groepen (NSG)
Ga als volgt Hallo [besturingselement binnenkomend verkeer documentatie](app-service-app-service-environment-control-inbound-traffic.md) voor meer informatie over het beperken van verkeer tooyour App Service-omgeving van Hallo WAF alleen met behulp van Hallo VIP-adres van uw Cloud-Service. Hier volgt een voorbeeld-Powershell-opdracht voor het uitvoeren van deze taak voor TCP-poort 80.

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Hallo SourceAddressPrefix vervangen door Hallo virtueel IP-adres (VIP) van uw WAF-Cloudservice.

> Opmerking: Hallo VIP van uw Cloud-Service wordt gewijzigd wanneer u verwijderen en opnieuw Hallo Service in de Cloud maken. Zorg ervoor dat tooupdate Hallo IP-adres in Hallo netwerk resourcegroep zodra u doet dit. 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png

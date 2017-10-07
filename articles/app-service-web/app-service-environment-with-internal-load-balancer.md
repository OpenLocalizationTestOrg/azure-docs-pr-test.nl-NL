---
title: aaaCreating en het gebruik van een interne Load Balancer met een App Service-omgeving | Microsoft Docs
description: Maken en gebruiken van een as-omgeving met een ILB
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: ad9a1e00-d5e5-413e-be47-e21e5b285dbf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 20799f260993d6e81499408e5b547a2e21430174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a>Met behulp van een interne Load Balancer met een App Service-omgeving

> [!NOTE] 
> In dit artikel gaat over het Hallo v1 App Service-omgeving. Er is een nieuwere versie van App Service-omgeving die eenvoudiger toouse en wordt uitgevoerd op krachtiger infrastructuur Hallo. meer informatie over de nieuwe versie Hallo met Hallo beginnen toolearn [inleiding toohello App Service-omgeving](../app-service/app-service-environment/intro.md).
>

Hallo as-omgeving (App Service omgeving)-functie is de optie voor een Premium-service van Azure App Service, die zorgt voor een verbeterde functie die is niet beschikbaar in Hallo multitenant stempels. Hallo as-omgeving functie wordt in wezen hello Azure App Service in uw virtuele Azure-Network(VNet) implementeert. toogain een beter inzicht in Hallo mogelijkheden die worden aangeboden door App Service-omgevingen lezen Hallo [wat is er een App-serviceomgeving] [ WhatisASE] documentatie. Als u niet Hallo voordelen weet van het besturingssysteem in een VNet lezen Hallo [virtuele netwerk Veelgestelde vragen over Azure][virtualnetwork]. 

## <a name="overview"></a>Overzicht
Een as-omgeving kan worden geïmplementeerd met een internet toegankelijk eindpunt of met een IP-adres in uw VNet. In de volgorde tooset Hallo IP-adres tooa VNet adres u uw as-omgeving met een interne Load Balancer(ILB) toodeploy nodig. Wanneer uw as-omgeving is geconfigureerd met een ILB moet u het volgende opgeven:

* uw eigen domein of subdomein. toomake eenvoudig dit document wordt ervan uitgegaan dat subdomein maar u kunt deze configureren in beide gevallen. 
* Hallo-certificaat dat wordt gebruikt voor HTTPS
* DNS-beheer voor een subdomein. 

Tegenprestatie kunt u doen, zoals:

* host intranettoepassingen, zoals line-of-business-toepassingen, veilig in Hallo cloud welke u toegang tot en met een Site tooSite of ExpressRoute VPN
* host-apps in Hallo cloud die niet worden weergegeven in de openbare DNS-servers
* maken van internet geïsoleerd back-end voor apps die uw apps front-end kunnen veilig worden geïntegreerd met

#### <a name="disabled-functionality"></a>Uitgeschakelde functionaliteit
Er zijn een aantal zaken die u niet mogelijk wanneer u een ILB-as-omgeving. Die dingen zijn onder andere:

* met behulp van IPSSL
* IP-adressen toewijzen toospecific apps
* kopen en gebruik van een certificaat met een app via Hallo-portal. U kunt uiteraard nog steeds certificaten rechtstreeks met een certificeringsinstantie verkrijgen en deze gebruiken met uw apps, niet via hello Azure-portal.

## <a name="creating-an-ilb-ase"></a>Een as ILB-omgeving maken
Maken van een as ILB-omgeving is niet veel verschillende normaal gesproken een as-omgeving maakt. Lees voor meer gedetailleerde informatie over het maken van een as-omgeving [hoe tooCreate een App-serviceomgeving][HowtoCreateASE]. Hallo proces toocreate een ILB-as-omgeving is Hallo dezelfde tussen het maken van een VNet tijdens het maken van de as-omgeving of een bestaande VNet te selecteren. toocreate een ILB-as-omgeving: 

1. In Azure portal Selecteer Hallo **Nieuw -> Web en mobiel -> App Service-omgeving**
2. Selecteer uw abonnement
3. Selecteer of maak een resourcegroep
4. Selecteer of maak een VNet
5. Een subnet maken als een VNet selecteren
6. Selecteer **virtuele netwerklocatie-VNet-configuratie >** en set Hallo VIP Type tooInternal
7. Geef de subdomeinnaam (dit zijn Hallo subdomein gebruikt voor apps die zijn gemaakt in deze as-omgeving)
8. Klik op Ok en maak vervolgens

![][1]

Er is een VNet-configuratie-optie binnen de blade virtueel netwerk Hallo. Dit kunt u kiezen tussen een externe VIP of interne VIP. Hallo standaard is extern. Als u hebt ingesteld tooExternal gebruik uw as-omgeving een internet toegankelijk VIP. Als u interne selecteert, wordt uw as-omgeving worden geconfigureerd met een ILB op een IP-adres binnen uw VNet. 

Na het selecteren van interne Hallo mogelijkheid tooadd meer IP-adressen tooyour die as-omgeving wordt verwijderd en in plaats daarvan moet u tooprovide Hallo subdomein van Hallo as-omgeving. Naam van het Hallo-as-omgeving wordt in een as-omgeving met een externe VIP-Hallo in Hallo subdomein gebruikt voor apps die zijn gemaakt in die as-omgeving. Als u uw as-omgeving is aangeroepen ***contosotest*** en de naam van uw app in die as-omgeving ***mytest*** wordt Hallo subdomein zou Hallo indeling ***contosotest.p.azurewebsites.net*** en Hallo-URL voor die app zou worden ***mytest.contosotest.p.azurewebsites.net***. Als u Hallo VIP Type tooInternal instelt, wordt de naam van uw as-omgeving niet gebruikt in Hallo subdomein voor Hallo as-omgeving. U opgeven Hallo subdomein expliciet. Als een subdomein is ***contoso.corp.net*** en u een app hebt aangebracht in de betreffende as-omgeving met de naam ***timereporting*** vervolgens Hallo URL voor die app zou worden ***timereporting.contoso.corp.net***.

## <a name="apps-in-an-ilb-ase"></a>Apps in een ILB-as-omgeving
Maken van een app in een ILB-as-omgeving is hetzelfde als voor het maken van een app in een as-omgeving is het normaal Hallo. 

1. In Azure portal Selecteer Hallo **Nieuw -> Web en mobiel -> Web** of **Mobile** of **API-App**
2. Voer de naam van app
3. Abonnement selecteren
4. Selecteer of resourcegroep maken
5. Selecteer of maak Plan(ASP) van App Service. Als uw as-omgeving als Hallo locatie en selecteer Hallo werknemersgroep maken van een nieuwe ASP vervolgens selecteert u uw ASP toobe gemaakt in. Wanneer u Hallo ASP maken selecteert u uw as-omgeving als Hallo locatie en Hallo werknemersgroep. Wanneer u de naam Hallo van Hallo app ziet u dat subdomein hello onder is de appnaam van uw vervangen door Hallo subdomein voor uw as-omgeving. 
6. Selecteer maken. U moet selecteren Hallo **pincode toodashboard** selectievakje in als u Hallo app tooshow op uw dashboard. 

![][2]

Onder Hallo app opgehaald naam Hallo subdomeinnaam bijgewerkte tooreflect Hallo subdomein van de as-omgeving. 

## <a name="post-ilb-ase-creation-validation"></a>Validatie van post ILB as-omgeving maken
Er is een ILB-as-omgeving iets anders dan Hallo niet - ILB as-omgeving. Als al opgemerkt u uw eigen DNS toomanage moet u ook tooprovide uw eigen certificaat hebben voor HTTPS-verbindingen. 

Nadat u uw as-omgeving maken ziet u dat subdomein Hallo Hallo subdomein toont u hebt opgegeven en er is een nieuw item in Hallo **instelling** menu aangeroepen **ILB certificaat**. Hallo as-omgeving wordt gemaakt met een zelfondertekend certificaat, waardoor het gemakkelijker tootest HTTPS. Hallo portal laat u weten dat u tooprovide uw eigen certificaat nodig voor HTTPS, maar dit toodrive is toohave een certificaat dat bij een subdomein hoort. 

![][3]

Als u gewoon things probeert uit en u niet hoe toocreate een certificaat weet, kunt u IIS MMC Hallo console toepassing toocreate een zelf-ondertekend certificaat. U kunt dit exporteren als een .pfx-bestand en vervolgens uploaden in Hallo ILB certificaat UI zodra deze is gemaakt. Wanneer u toegang tot een site die is beveiligd met een zelfondertekend certificaat, uw browser, krijgt u een waarschuwing dat u toegang tot site Hallo is niet beveiligd vanwege toohello onvermogen toovalidate Hallo certificaat. Als u deze waarschuwing tooavoid wilt, moet u een correct ondertekende certificaat die overeenkomt met een subdomein en heeft een vertrouwensketen die door uw browser is herkend.

![][6]

Als u wilt dat tootry hello-stromen met uw eigen certificaten en testen van HTTP en HTTPS toegang tooyour as-omgeving:

1. Ga tooASE UI nadat as-omgeving is gemaakt **as-omgeving -> Instellingen -> ILB certificaten**
2. ILB certificaat ingesteld door het pfx-certificaatbestand selecteren en wachtwoord opgeven. Deze stap duurt enigszins tijdens tooprocess en het Hallo-bericht dat een vergroten/verkleinen uitgevoerd wordt, worden weergegeven.
3. Hallo ILB adres ophalen voor uw as-omgeving (**as-omgeving -> Eigenschappen van virtuele IP-adres ->**)
4. Een WebApp maken in de as-omgeving na het maken 
5. Een virtuele machine maken als u niet in dit VNET hebt (Hallo niet in hetzelfde subnet als Hallo as-omgeving of dingen break)
6. DNS instellen voor een subdomein. U kunt een jokerteken worden gebruikt met een subdomein in uw DNS of als u enkele eenvoudige tests uit, toodo wilt bewerken Hallo hosts-bestand op uw VM tooset web app name tooVIP IP-adres. Als uw as-omgeving had Hallo subdomeinnaam. ilbase.com en u web-app mytestapp Hallo zodat zou worden aangepakt op mytestapp.ilbase.com vervolgens ingesteld die in het hosts-bestand gemaakt. (In Windows hello hosts-bestand is op C:\Windows\System32\drivers\etc\)
7. Een browser gebruiken die op deze virtuele machine en ga toohttp://mytestapp.ilbase.com (of wat de naam van uw web-app met een subdomein is)
8. Een browser gebruiken die op deze virtuele machine en ga toohttps://mytestapp.ilbase.com hebt uitgevoerd, tooaccept Hallo gebrek aan beveiliging als een zelfondertekend certificaat gebruikt. 

Hallo IP-adres voor de ILB wordt vermeld in de eigenschappen van uw als Hallo virtueel IP-adres

![][4]

## <a name="using-an-ilb-ase"></a>Met behulp van een as ILB-omgeving
#### <a name="network-security-groups"></a>Netwerkbeveiligingsgroepen
Een ILB as-omgeving kunt netwerkisolatie voor uw apps zoals Hallo apps zijn niet toegankelijk of zelfs door bekende Hallo internet. Dit is een uitstekende voor het hosten van websites op het intranet zoals line-of-business-toepassingen. Wanneer u toorestrict toegang zelfs nodig kunt verder u Network Security Groups(NSGs) toocontrol toegang op Hallo niveau. 

Indien gewenst toouse nsg's toofurther toegang beperken moet u ervoor dat verbreekt u niet Hallo communicatie toomake nodig volgorde toooperate die as Hallo-omgeving heeft. Hoewel Hallo HTTP/HTTPS-toegang beperken tot Hallo ILB gebruikt door Hallo as-omgeving Hallo die as-omgeving nog steeds gebruik van resource buiten Hallo VNet. bekijkt hello informatie in Hallo document toosee welke netwerktoegang is nog steeds vereist op [binnenkomend verkeer beheren tooan App Service-omgeving] [ ControlInbound] en het Hallo-document op [netwerk Configuratiedetails voor App Service-omgevingen met ExpressRoute][ExpressRoute]. 

tooconfigure uw nsg's moet u tooknow Hallo IP adres dat wordt gebruikt door Azure toomanage uw as-omgeving. Dat IP-adres is ook Hallo uitgaande IP-adres uit de as-omgeving als aanvragen voor internet maakt. Hallo uitgaande IP-adres voor uw as-omgeving blijft statische voor Hallo levensduur van de as-omgeving. Als u verwijderen en opnieuw maken van uw as-omgeving, krijgt u een nieuw IP-adres. Dit IP-adres te gaan toofind**instellingen -> eigenschappen** en Hallo zoeken **uitgaande IP-adres**. 

![][5]

#### <a name="general-ilb-ase-management"></a>Beheer van algemene ILB as-omgeving
Het beheren van een as ILB-omgeving is nog grotendeels Hallo hetzelfde als normaal gesproken een as-omgeving beheren geweest. U moet tooscale van uw pools worker toohost meer exemplaren van de ASP- en opschalen uw Front-End servers toohandle grotere hoeveelheden HTTP/HTTPS-verkeer. Voor algemene informatie over het Hallo-configuratie van een as-omgeving beheren door Hallo document te lezen op [configureren van een App-serviceomgeving][ASEConfig]. 

Hallo extra items zijn Certificaatbeheer en DNS-beheer. U moet tooobtain en upload Hallo certificaat gebruikt voor HTTPS na het maken van de ILB as-omgeving en vervang deze voordat deze verloopt. Omdat Azure eigenaar is van het basisdomein Hallo bieden we certificaten voor ASEs met een externe VIP. Aangezien Hallo subdomein gebruikt door een ILB-as-omgeving van alles zijn kan, moet u op tooprovide uw eigen certificaat voor HTTPS. 

#### <a name="dns-configuration"></a>DNS-configuratie
Als u een externe VIP Hallo die DNS wordt beheerd door Azure. Elke app gemaakt in uw as-omgeving wordt automatisch tooAzure DNS die een openbare DNS-server is toegevoegd. In een ILB-as-omgeving hebt u toomanage uw eigen DNS. Voor een bepaalde subdomein zoals contoso.corp.net moet u toocreate die DNS A-records dat punt tooyour ILB-adres voor:

    * 
    *.SCM ftp publiceren 


## <a name="getting-started"></a>Aan de slag
Alle artikelen en hoe-aan de voor App Service-omgevingen beschikbaar in Hallo zijn [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).

tooget de slag met App Service-omgevingen, Zie [inleiding tooApp Service-omgevingen][WhatisASE]

Zie voor meer informatie over hello Azure App Service-platform, [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createilbase.png
[2]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createapp.png
[3]: ./media/app-service-environment-with-internal-load-balancer/ilbase-newase.png
[4]: ./media/app-service-environment-with-internal-load-balancer/ilbase-vip.png
[5]: ./media/app-service-environment-with-internal-load-balancer/ilbase-externalvip.png
[6]: ./media/app-service-environment-with-internal-load-balancer/ilbase-ilbcertificate.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[vnetnsgs]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/

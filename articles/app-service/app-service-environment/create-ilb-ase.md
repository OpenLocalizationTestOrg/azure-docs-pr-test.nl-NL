---
title: aaaCreate en het gebruik van een interne load balancer met een Azure App Service-omgeving
description: "Meer informatie over het toocreate en gebruik van een geïsoleerd van internet Azure App Service-omgeving"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a>Maken en gebruiken van een interne load balancer met een App Service-omgeving #

 Azure App Service-omgeving is een implementatie van Azure App Service in een subnet in een Azure-netwerk (VNet). Er zijn twee manieren toodeploy een App Service-omgeving (as-omgeving): 

- Een VIP-adres op een externe IP-adres, vaak aangeduid als een externe as-omgeving.
- Een VIP-adres op een interne IP-adres, vaak genoemd, een ILB-as-omgeving omdat Hallo interne eindpunt, een interne load balancer (ILB is). 

Dit artikel ziet u hoe toocreate een ILB-as-omgeving. Zie voor een overzicht op Hallo as-omgeving [inleiding tooApp Service-omgevingen][Intro]. hoe toocreate een externe as-omgeving, Zie toolearn [maken van een externe as-omgeving][MakeExternalASE].

## <a name="overview"></a>Overzicht ##

U kunt een as-omgeving met een internet toegankelijke eindpunt of met een IP-adres implementeren in uw VNet. tooset hello IP-adressen tooa VNet-adres, Hallo as-omgeving moet worden geïmplementeerd met een ILB. Wanneer u uw as-omgeving met een ILB implementeert, moet u het volgende opgeven:

-   Uw eigen domein dat u bij het maken van uw apps.
-   Hallo-certificaat gebruikt voor HTTPS.
-   DNS-beheer voor uw domein.

Tegenprestatie kunt u doen, zoals:

-   Intranet-hosttoepassingen veilig in Hallo cloud, die u via een site-naar-site of Azure ExpressRoute VPN-toegang.
-   Host-apps in Hallo cloud die niet zijn opgenomen in de openbare DNS-servers.
-   Internet geïsoleerd back-end-apps, die uw front-apps kunnen veilig worden geïntegreerd met maken.

### <a name="disabled-functionality"></a>Uitgeschakelde functionaliteit ###

Er zijn een aantal zaken die u niet mogelijk wanneer u een ILB-as-omgeving:

-   IP-gebaseerde SSL wordt gebruikt.
-   IP-adressen toewijzen toospecific apps.
-   Koop en een certificaat met een app via hello Azure-portal gebruiken. U kunt certificaten rechtstreeks vanuit een certificeringsinstantie verkrijgen en ze gebruiken met uw apps. U kunt deze kan niet verkrijgen via hello Azure-portal.

## <a name="create-an-ilb-ase"></a>Een as ILB-omgeving maken ##

toocreate een ILB-as-omgeving:

1. Selecteer in de Azure-portal hello, **nieuw** > **Web en mobiel** > **App Service-omgeving**.

2. Selecteer uw abonnement.

3. Selecteer of maak een resourcegroep.

4. Selecteer of maak een VNet.

5. Als u een bestaande VNet selecteert, moet u toocreate een subnet toohold Hallo as-omgeving. Zorg ervoor dat eventuele toekomstige groei van uw as-omgeving voor grootte groot genoeg tooaccommodate tooset een subnet. Een grootte van het is raadzaam `/25`, waardoor 128 adressen heeft en een maximale grootte as-omgeving kan verwerken. is de minimale grootte Hallo kunt u een `/28`. Nadat de infrastructuur nodig heeft, kan de grootte van deze geschaalde tooa maximaal 11 exemplaren zijn.

    * Verder dan Hallo standaardaantal van maximaal 100 exemplaren in uw App Service-abonnementen.

    * In de buurt van 100, maar met meer snelle front-schaling schalen.

6. Selecteer **virtuele netwerklocatie** > **virtuele netwerkconfiguratie**. Set Hallo **VIP Type** te**intern**.

7. Voer de domeinnaam van een. Dit domein is Hallo gebruikt voor apps die zijn gemaakt in deze as-omgeving. Er zijn enkele beperkingen. Kan niet worden:

    * NET   

    * azurewebsites.NET

    * p.azurewebsites.NET

    * &lt;asename&gt;. p.azurewebsites.net

   de aangepaste domeinnaam Hallo gebruikt voor apps en Hallo-domeinnaam die wordt gebruikt door uw as-omgeving kunnen elkaar niet overlappen. Voor een as ILB-omgeving met de domeinnaam Hallo _contoso.com_, u kunt aangepaste domeinnamen voor uw apps zoals niet gebruiken:

    * www.contoso.com

    * ABCD.def.contoso.com

    * ABCD.contoso.com

   Als u Hallo aangepaste domeinnamen voor uw apps weet, kiest u een domein voor Hallo as-ILB omgeving die u geen een conflict met deze aangepaste domeinnamen hebt. In dit voorbeeld kunt u ongeveer *contoso internal.com* voor Hallo domein van uw as-omgeving omdat dat geen met aangepaste domeinnamen die eindigen conflicten op *. contoso.com*.

8. Selecteer **OK**, en selecteer vervolgens **maken**.

    ![ASE maken][1]

Op Hallo **virtueel netwerk** blade, er is een **virtuele netwerkconfiguratie** optie. U kunt deze gebruiken tooselect een externe VIP of een interne VIP. Hallo standaardwaarde is **externe**. Als u selecteert **externe**, uw as-omgeving maakt gebruik van een internet toegankelijke VIP. Als u selecteert **intern**, uw as-omgeving is geconfigureerd met een ILB op een IP-adres binnen uw VNet.

Nadat u hebt geselecteerd **intern**, Hallo mogelijkheid tooadd meer IP-adressen tooyour as-omgeving wordt verwijderd. In plaats daarvan moet u tooprovide Hallo domein Hallo as-omgeving. In een as met een externe VIP-omgeving, wordt hello naam van het Hallo-as-omgeving gebruikt in Hallo domein voor apps die zijn gemaakt in die as-omgeving.

Als u instelt **VIP Type** te**intern**, de naam van uw as-omgeving wordt niet gebruikt in Hallo domein voor Hallo as-omgeving. U opgeven expliciet Hallo domein. Als uw domein *contoso.corp.net* en u een app maken in de betreffende as-omgeving met de naam *timereporting*, Hallo URL voor die app timereporting.contoso.corp.net is.


## <a name="create-an-app-in-an-ilb-ase"></a>Een app maken in een ILB-as-omgeving ##

U een app maken in een ILB-as-omgeving in Hallo dezelfde manier waarop u een app in een as-omgeving normaal.

1. Selecteer in de Azure-portal hello, **nieuw** > **Web en mobiel** > **Web** of **Mobile** of  **API-App**.

2. Voer de naam Hallo van Hallo-app.

3. Hallo-abonnement selecteren.

4. Selecteer of maak een resourcegroep.

5. Selecteer of maak een App Service-abonnement. Als u een nieuw App Service-plan toocreate wilt, selecteert u uw as-omgeving als Hallo locatie. Selecteer Hallo werknemersgroep waar u uw App Service-plan toobe gemaakt. Wanneer u Hallo App Service-abonnement hebt gemaakt, selecteert u uw as-omgeving als Hallo locatie en Hallo werknemersgroep. Wanneer u Hallo-naam van Hallo app opgeeft, is Hallo domein onder de appnaam van uw vervangen door Hallo domein voor uw as-omgeving.

6. Selecteer **Maken**. Als u Hallo app tooappear op uw dashboard, selecteert de **pincode toodashboard** selectievakje.

    ![App Service-abonnement maken][2]

    Onder **appnaam**, Hallo domeinnaam is bijgewerkte tooreflect Hallo domein van uw as-omgeving.

## <a name="post-ilb-ase-creation-validation"></a>Validatie van post ILB as-omgeving maken ##

Er is een ILB-as-omgeving iets anders dan Hallo niet - ILB as-omgeving. Als al hebt genoteerd moet u toomanage uw eigen DNS. Hebt u ook tooprovide uw eigen certificaat voor HTTPS-verbindingen.

Nadat u uw as-omgeving hebt gemaakt, toont domeinnaam Hallo Hallo door u opgegeven domein. Een nieuw item wordt weergegeven in de **instelling** menu aangeroepen **ILB certificaat**. Hallo as-omgeving wordt gemaakt met een certificaat dat niet Hallo ILB as-omgeving domein opgeven. Als u Hallo as-omgeving met dat certificaat gebruikt, wordt uw browser aangegeven dat het is ongeldig. Dit certificaat maakt het eenvoudiger tootest HTTPS, maar u moet tooupload uw eigen certificaat dat is gebonden tooyour ILB as-omgeving domein. Deze stap is nodig, ongeacht of het certificaat is zelfondertekend of verkregen via een certificeringsinstantie.

![De domeinnaam ILB as-omgeving][3]

Uw as ILB-omgeving moet een geldig SSL-certificaat. Interne CA's gebruiken, een certificaat kopen bij een externe verlener of een zelfondertekend certificaat gebruiken. Ongeacht Hallo bron van het SSL-certificaat hello moeten hello volgende kenmerken van het certificaat toobe correct is geconfigureerd:

* **Onderwerp**: dit kenmerk too*.your, root, domein, hier moet worden ingesteld.
* **Alternatieve onderwerpnaam**: dit kenmerk moet bevatten beide **.your, root, domein, hier* en **.scm.your-hoofdmap-domain-hier*. SSL-verbindingen toohello SCM/Kudu site die is gekoppeld aan elke app gebruiken een adres van het formulier Hallo *your-app-name.scm.your-root-domain-here*.

Hallo SSL-certificaat, converteren/opslaan als een .pfx-bestand. Hallo pfx-bestand moet alle tussenliggende bevatten en de hoofd-certificaten. Beveilig deze met een wachtwoord.

Als u een zelfondertekend certificaat toocreate wilt, kunt u hier Hallo PowerShell-opdrachten gebruiken. Worden toouse ervoor dat de domeinnaam van uw ILB as-omgeving in plaats van *internal.contoso.com*: 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

Hallo-certificaat dat u deze PowerShell-opdrachten genereren is gemarkeerd door browsers omdat Hallo-certificaat is niet gemaakt door een certificeringsinstantie die in de vertrouwensketen van uw browser. tooget een certificaat dat door uw browser vertrouwt, schaft u deze via een commerciële certificeringsinstantie in de vertrouwensketen van uw browser. 

![Set ILB certificaat][4]

tooupload uw eigen certificaten en toegang testen:

1. Nadat het Hallo-as-omgeving is gemaakt, gaat u toohello UI as-omgeving. Selecteer **as-omgeving** > **instellingen** > **ILB certificaat**.

2. tooset hello ILB certificaat Hallo certificate pfx-bestand selecteren en Hallo wachtwoord invoeren. Deze stap duurt enkele tooprocess tijd. Er verschijnt een bericht dat een uploadbewerking uitgevoerd wordt.

3. Hallo ILB adres ophalen voor uw as-omgeving. Selecteer **as-omgeving** > **eigenschappen** > **virtueel IP-adres**.

4. Een web-app maken in uw as-omgeving nadat Hallo as-omgeving is gemaakt.

5. Een virtuele machine maken als u niet in dit VNet hebt.

    > [!NOTE] 
    > Probeer niet toocreate deze virtuele machine in hetzelfde subnet Hallo zoals Hallo as-omgeving, omdat deze wordt niet uitgevoerd of problemen veroorzaken.
    >
    >

6. Hallo DNS voor uw domein as-omgeving instellen. U kunt een jokerteken gebruiken met uw domein in uw DNS. toodo enkele eenvoudige tests, Hallo hosts-bestand op uw VM tooset Hallo web app name toohello VIP IP-adres bewerken:

    a. Als uw as-omgeving Hallo domeinnaam heeft _. ilbase.com_ en maken van Hallo web-app met de naam _mytestapp_, het gericht op _mytestapp.ilbase.com_. Vervolgens stelt u _mytestapp.ilbase.com_ tooresolve toohello ILB adres. (Op Windows hello hostbestand loopt _C:\Windows\System32\drivers\etc\_.)

    b. tootest web deployment publishing of toegang toohello, geavanceerde console, maakt u een record voor _mytestapp.scm.ilbase.com_.

7. Een browser gebruiken die op deze virtuele machine en Ga naar http://mytestapp.ilbase.com. (Of de naam van uw web-app met uw domein is toowhatever gaat.)

8. Een browser gebruiken die op deze virtuele machine en Ga naar https://mytestapp.ilbase.com. Als u een zelfondertekend certificaat gebruikt, accepteert u Hallo gebrek aan beveiliging.

    Hallo IP-adres voor de ILB wordt vermeld onder **IP-adressen**. Deze lijst heeft ook Hallo IP-adressen die door externe VIP Hallo en voor binnenkomende beheer van verkeer.

    ![ILB IP-adres][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a>Web-taken, functies en Hallo ILB as-omgeving

Zowel functies en webtaken worden ondersteund op een as ILB-omgeving, maar voor Hallo portal toowork met hen, moet u toegang toohello SCM netwerksite hebben.  Dit betekent dat de browser moet op een host die zich in of toohello virtueel netwerk is verbonden.  

Als u Azure Functions op een as ILB-omgeving gebruikt, krijgt u mogelijk een foutbericht weergegeven waarin wordt gemeld 'We kunnen niet kunnen tooretrieve momenteel door uw functies. Probeer het later opnieuw." Deze fout treedt op omdat Hallo functies UI maakt gebruik van Hallo SCM site via HTTPS en het Hallo-basiscertificaat niet in Hallo browser vertrouwensketen wordt. Webtaken heeft een soortgelijk probleem. tooavoid dit probleem kunt u een van de volgende Hallo doen:

- Hallo certificaat tooyour vertrouwde certificaatarchief toevoegen. Dit blokkering opgeheven rand en Internet Explorer.
- Chrome gebruiken en ga toohello SCM eerst, niet-vertrouwd certificaat Hallo accepteren en gaat u toohello-portal.
- Een commerciële certificaat in uw browser vertrouwensketen gebruiken.  Dit is de beste optie Hallo.  

## <a name="dns-configuration"></a>DNS-configuratie ##

Wanneer u een externe VIP gebruikt, wordt door Azure DNS Hallo beheerd. Elke app gemaakt in uw as-omgeving automatisch toegevoegd tooAzure DNS, dit is een openbare DNS-server. In een ILB as-omgeving, moet u uw eigen DNS beheren. Voor een bepaald domein, zoals _contoso.net_, moet u toocreate DNS A-records in DNS dat punt tooyour ILB-adres voor:

- *. contoso.net
- *. scm.contoso.net

Als uw domein ILB as-omgeving wordt gebruikt voor meerdere dingen buiten deze as-omgeving, moet u mogelijk toomanage DNS op basis van de per-app-naam. Deze methode is lastig omdat u nodig tooadd elke nieuwe appnaam in uw DNS hebt wanneer u deze maakt. Daarom is het raadzaam dat u een speciale domein.

## <a name="publish-with-an-ilb-ase"></a>Publiceren met een ILB-as-omgeving ##

Voor elke app die gemaakt, zijn er twee eindpunten. In een ILB as-omgeving, hebt u  *&lt;app-naam >.&lt; ILB as-omgeving Domain >* en  *&lt;app-naam > .scm.&lt; ILB as-omgeving Domain >*. 

Hallo SCM-sitenaam gaat u verder toohello Kudu-console, aangeroepen Hallo **geavanceerde portal**in hello Azure-portal. Hallo Kudu-console kunt u omgevingsvariabelen weergeven, Hallo schijf verkennen, gebruikt u een console, en nog veel meer. Zie voor meer informatie [Kudu-console voor Azure App Service][Kudu]. 

Er is eenmalige aanmelding tussen hello Azure-portal en Hallo Kudu-console in Hallo multitenant-App Service en in een externe as-omgeving. Voor Hallo ILB as-omgeving, maar moet u toouse uw publishing referenties toosign in Hallo Kudu-console.

Internetgebaseerde CI systemen, zoals GitHub en Visual Studio Team Services, werkt niet met een ILB-as-omgeving omdat publishing Hallo-eindpunt niet toegankelijk internet. In plaats daarvan moet u een CI-besturingssysteem dat gebruikmaakt van een pull-model, zoals Dropbox toouse.

Hallo publishing eindpunten voor apps in een ILB-as-omgeving gebruik Hallo domein dat Hallo die ILB as-omgeving is gemaakt met. Dit domein wordt weergegeven in het publicatieprofiel Hallo-app en op de portalblade van Hallo app (**overzicht** > **Essentials** en ook **eigenschappen**). Als u een ILB-as-omgeving met Hallo subdomein hebt *contoso.net* en een app met de naam *mytest*, gebruik *mytest.contoso.net* voor FTP en *mytest.scm.contoso.net*  voor implementatie.

## <a name="couple-an-ilb-ase-with-a-waf-device"></a>Combineer een ILB-as-omgeving met een WAF-apparaat ##

Azure App Service biedt veel beveiligingsfuncties die Hallo systeem te beschermen. Ze helpen ook toodetermine of een app gehackte is. Hallo beste beveiliging voor een webtoepassing is toocouple een host-platform, zoals Azure App Service met een web application firewall (WAF). Omdat Hallo ILB as-omgeving een toepassingseindpunt netwerk geïsoleerd van heeft, is het geschikt is voor dit gebruik.

meer informatie over hoe tooconfigure uw as ILB-omgeving met een apparaat WAF zien toolearn [web application firewall configureren met uw App-serviceomgeving][ASEWAF]. Dit artikel laat zien hoe toouse een virtueel apparaat Barracuda met uw as-omgeving. Een andere optie is toouse Azure Application Gateway. Toepassingsgateway maakt gebruik van Hallo OWASP core regels toosecure toepassingen erachter geplaatst. Zie voor meer informatie over Application Gateway [inleiding toohello Azure-web application firewall][AppGW].

## <a name="get-started"></a>Aan de slag ##

Alle artikelen en hoe-tooinstructions voor ASEs zijn beschikbaar in de [Leesmij-bestand voor App Service-omgevingen][ASEReadme].

* tooget gestart met ASEs, Zie [inleiding tooApp Service-omgevingen][Intro].
* Zie voor meer informatie over hello Azure App Service-platform, [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md

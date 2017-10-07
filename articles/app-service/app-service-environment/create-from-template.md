---
title: aaaCreate een Azure App Service-omgeving met een Resource Manager-sjabloon
description: Legt uit hoe toocreate een externe of ILB Azure App Service-omgeving met een Resource Manager-sjabloon
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: c8aeedee675a6e931169b725ee916cc7fa8f762f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a>Een as-omgeving maken met een Azure Resource Manager-sjabloon

## <a name="overview"></a>Overzicht
Azure App Service-omgevingen (ASEs) kunnen worden gemaakt met een eindpunt toegankelijk is via het internet of een eindpunt op een intern adres in een Azure-netwerk (VNet). Wanneer dit wordt gemaakt met een interne eindpunt, wordt dat eindpunt wordt verstrekt door een Azure onderdeel een interne load balancer (ILB) genoemd. Hallo as-omgeving op een interne IP-adres, heet een ILB-as-omgeving. Hallo as-omgeving met een openbaar eindpunt heet een externe as-omgeving. 

Een as-omgeving kan worden gemaakt met behulp van hello Azure-portal of een Azure Resource Manager-sjabloon. In dit artikel wordt uitgelegd Hallo stappen en de syntaxis die u moet toocreate een externe as-omgeving of ILB as-omgeving met Resource Manager-sjablonen. hoe toocreate een as-omgeving in hello Azure-portal, Zie toolearn [maken van een externe as-omgeving] [ MakeExternalASE] of [maken van een as ILB-omgeving][MakeILBASE].

Wanneer u een as-omgeving in hello Azure-portal maakt, kunt u uw VNet maken op Hallo dezelfde tijd of kies een bestaande VNet toodeploy in. Wanneer u een as-omgeving van een sjabloon maakt, moet u beginnen met: 

* Een Resource Manager VNet.
* Een subnet in dit VNet. De grootte van een as-omgeving van het is raadzaam `/25` met 128 adressen tooaccomodate toekomstige groei. Nadat Hallo as-omgeving is gemaakt, kunt u Hallo grootte niet wijzigen.
* Hallo resource-ID van uw VNet. U kunt deze informatie vinden in hello Azure-portal onder de eigenschappen van uw virtuele netwerk.
* Hallo-abonnement die u wilt dat toodeploy in.
* gewenste toodeploy in Hallo-locatie.

tooautomate uw as-omgeving maken:

1. Hallo-as-omgeving met een sjabloon maken. Als u een externe as-omgeving maakt, bent u klaar na deze stap. Als u een ILB-as-omgeving maakt, zijn er enkele meer dingen toodo.

2. Nadat u uw as ILB-omgeving is gemaakt, wordt een SSL-certificaat dat overeenkomt met uw domein ILB as-omgeving geüpload.

3. Hallo is geüploade SSL-certificaat toegewezen toohello ILB as-omgeving als het SSL-certificaat 'standaard'.  Dit certificaat wordt gebruikt voor SSL-verkeer tooapps op Hallo ILB as-omgeving wanneer ze Hallo gemeenschappelijk hoofddomein dat is toegewezen toohello as-omgeving (bijvoorbeeld https://someapp.mycustomrootcomain.com) gebruiken.


## <a name="create-hello-ase"></a>Hallo-as-omgeving maken
Resource Manager-sjabloon die u een as-omgeving en de bijbehorende parameters-bestand maakt is beschikbaar [in een voorbeeld] [ quickstartasev2create] op GitHub.

Als u toomake een ILB-as-omgeving wilt, gebruikt u deze Resource Manager-sjabloon [voorbeelden][quickstartilbasecreate]. Ze voorzien toothat gebruiksvoorbeeld. De meeste van Hallo-parameters in Hallo *azuredeploy.parameters.json* bestand algemene toohello maken van ILB ASEs en externe ASEs zijn. Hallo hieronder illustreert parameters van speciale opmerking of die uniek zijn, zijn bij het maken van een as ILB-omgeving:

* *interalLoadBalancingMode*: Stel In de meeste gevallen deze too3, wat betekent zowel HTTPS-verkeer op poort 80/443 dat, en Hallo controlegegevens/channel-poorten geluisterd tooby Hallo FTP-service op Hallo as-omgeving, worden afhankelijke tooan ILB toegewezen virtueel netwerk interne adres. Als deze eigenschap is ingesteld too2, alleen Hallo FTP-service-gerelateerde poorten (zowel besturings- als kanalen) zijn gebonden tooan ILB adres. Hallo HTTP/HTTPS-verkeer blijft op Hallo openbare VIP.
* *dnsSuffix*: deze parameter bepaalt Hallo standaard hoofddomein dat is toegewezen toohello as-omgeving. In de openbare variatie op Hallo van Azure App Service, Hallo standaard hoofddomein voor alle web-apps is *azurewebsites.net*. Omdat een ILB-as-omgeving van de klant van de interne tooa virtueel netwerk, niet dat u zin toouse Hallo openbare van de service standaard hoofddomein. Een as ILB-omgeving moet in plaats daarvan een standaard-hoofddomein die zinvol voor gebruik binnen een bedrijf intern virtueel netwerk hebben. Bijvoorbeeld, Contoso Corporation gebruiken een hoofddomein standaard van *interne contoso.com* voor apps die bedoeld toobe omgezet en toegankelijk zijn alleen binnen het virtuele netwerk van Contoso zijn. 
* *ipSslAddressCount*: deze parameter standaard automatisch tooa waarde van 0 in Hallo *azuredeploy.json* bestand omdat ILB ASEs slechts één ILB-adres hebben. Er zijn geen expliciete SSL IP-adressen voor een as ILB-omgeving. Hallo SSL IP-adresgroep voor een as ILB-omgeving moet daarom toozero ingesteld. Anders treedt er een inrichten fout op. 

Na het Hallo *azuredeploy.parameters.json* bestand is ingevuld, Hallo as-omgeving maken met behulp van PowerShell-codefragment Hallo. Hallo paden toomatch Hallo Resource Manager-sjabloonbestand bestandslocaties op uw computer wijzigen. Houd rekening met toosupply uw eigen waarden voor implementatienaam Hallo-Resource Manager en Hallo de naam van resourcegroep:

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Het duurt ongeveer een uur Hallo as-omgeving toobe gemaakt. Vervolgens weergegeven Hallo as-omgeving in Hallo portal in de lijst Hallo van ASEs voor Hallo-abonnement dat Hallo implementatie geactiveerd.

## <a name="upload-and-configure-hello-default-ssl-certificate"></a>Uploaden en Hallo 'standaard' SSL-certificaat configureren
Een SSL-certificaat moet worden gekoppeld aan het Hallo-as-omgeving als Hallo 'standaard' SSL-certificaat dat is gebruikt tooestablish SSL-verbindingen tooapps. Als de as-omgeving Hallo standaard DNS-achtervoegsel *interne contoso.com*, een toohttps://some-random-app.internal-contoso.com verbinding vereist een SSL-certificaat is geldig voor **.internal contoso.com* . 

Een geldig SSL-certificaat ophalen met behulp van de interne CA's, een certificaat aanschaffen van een externe verlener of met behulp van een zelfondertekend certificaat. Ongeacht Hallo bron van Hallo SSL-certificaat, moet de Hallo volgende certificaat-kenmerken juist zijn geconfigureerd:

* **Onderwerp**: dit kenmerk te moet worden ingesteld **.your-hoofdmap-domain-here.com*.
* **Alternatieve onderwerpnaam**: dit kenmerk moet bevatten beide **.your-hoofdmap-domain-here.com* en **.scm.your-hoofdmap-domain-here.com*. SSL-verbindingen toohello SCM/Kudu site die is gekoppeld aan elke app gebruiken een adres van het formulier Hallo *your-app-name.scm.your-root-domain-here.com*.

Met een geldig SSL-certificaat in de hand, worden twee aanvullende voorbereidende stappen uitgevoerd. Hallo SSL-certificaat, converteren/opslaan als een .pfx-bestand. Houd er rekening mee dat Hallo pfx-bestand moet bevatten alle tussenliggende en de hoofd-certificaten. Beveilig deze met een wachtwoord.

Hallo pfx-bestand moet toobe geconverteerd naar een base64-tekenreeks omdat de SSL-certificaat hello wordt geüpload met behulp van een Resource Manager-sjabloon. Omdat Resource Manager-sjablonen tekstbestanden zijn, kan Hallo pfx-bestand moet worden geconverteerd naar een base64-tekenreeks. Op deze manier kan zijn als een parameter van het Hallo-sjabloon opgenomen.

Hallo volgende PowerShell-codefragment om te gebruiken:

* Een zelfondertekend certificaat genereren.
* Hallo-certificaat exporteren als een .pfx-bestand.
* Hallo pfx-bestand worden geconverteerd naar een base64-gecodeerde tekenreeks.
* Hallo base64-gecodeerde tekenreeks tooa afzonderlijk bestand opslaan. 

Deze PowerShell-code voor base64-codering is gebaseerd op Hallo [PowerShell scripts blog][examplebase64encoding]:

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

Nadat Hallo SSL-certificaat wordt gegenereerd en geconverteerd tooa base64-gecodeerde tekenreeks, gebruikt u Hallo voorbeeld Resource Manager-sjabloon [Hallo standaard SSL-certificaat configureren] [ quickstartconfiguressl] op GitHub. 

Hallo-parameters in Hallo *azuredeploy.parameters.json* bestand worden hier vermeld:

* *appServiceEnvironmentName*: naam Hallo Hallo ILB as-omgeving wordt geconfigureerd.
* *existingAseLocation*: string met tekst hello Azure-regio waar hello ILB as-omgeving is geïmplementeerd.  Bijvoorbeeld: 'Zuid-centraal VS'.
* *pfxBlobString*: Hallo based64-gecodeerde tekenreeksrepresentatie van Hallo pfx-bestand. Gebruik Hallo codefragment hierboven en kopieer Hallo tekenreeks in 'exportedcert.pfx.b64'. Plak deze in als waarde Hallo Hallo *pfxBlobString* kenmerk.
* *wachtwoord*: Hallo serverwachtwoord toosecure Hallo pfx-bestand.
* *certificateThumbprint*: Hallo vingerafdruk van het certificaat. Als u deze waarde wordt opgehaald uit PowerShell (bijvoorbeeld *$certificate. Vingerafdruk* van Hallo eerdere codefragment), kunt u Hallo-waarde is. Als u Hallo-waarde van het dialoogvenster Windows-certificaat Hallo kopieert, vergeet dan niet toostrip uit Hallo overbodige spaties. Hallo *certificateThumbprint* ziet er ongeveer als AF3143EB61D43F6727842115BB7F17BBCECAECAE.
* *Certificaatnaam*: een beschrijvende tekenreeks-id van uw eigen keuze tooidentity Hallo certificaat gebruikt. Hallo-naam wordt gebruikt als onderdeel van Hallo unieke bronnenbeheerder-id voor Hallo *Microsoft.Web/certificates* entiteit die de SSL-certificaat Hallo vertegenwoordigt. de naam van de Hallo *moet* eindigen met het volgende achtervoegsel Hallo: \_yourASENameHere_InternalLoadBalancingASE. Dit achtervoegsel Hello Azure-portal gebruikt een indicator die Hallo certificaat is gebruikte toosecure een as ingeschakeld met een ILB-omgeving.

Een afgekorte voorbeeld van *azuredeploy.parameters.json* Hier wordt weergegeven:

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

Na het Hallo *azuredeploy.parameters.json* bestand is ingevuld, Hallo standaard SSL-certificaat configureren met behulp van PowerShell-codefragment Hallo. Hallo bestand paden toomatch waar Hallo Resource Manager-sjabloonbestanden op uw computer bevinden zich wijzigen. Houd rekening met toosupply uw eigen waarden voor implementatienaam Hallo-Resource Manager en Hallo de naam van resourcegroep:

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Het duurt ongeveer 40 minuten per as-omgeving front-end tooapply Hallo wijziging. Bijvoorbeeld, bij een standaardformaat as-omgeving die gebruikmaakt van twee front-ends, krijgt Hallo sjabloon rond één uur en 20 minuten toocomplete. Tijdens het Hallo-sjabloon wordt uitgevoerd, kan niet Hallo as-omgeving schalen.  

Nadat Hallo-sjabloon is voltooid, kan apps op Hallo ILB as-omgeving kunnen worden benaderd via HTTPS. Hallo-verbindingen zijn beveiligd met behulp van Hallo standaard SSL-certificaat. Hallo standaard SSL-certificaat wordt gebruikt wanneer de apps op Hallo ILB as-omgeving door een combinatie van naam van de toepassing hello plus Hallo standaardhostnaam worden aangepakt. Https://mycustomapp.internal-contoso.com gebruikt bijvoorbeeld Hallo standaard SSL-certificaat voor **.internal contoso.com*.

Ontwikkelaars kunnen echter net als bij apps die worden uitgevoerd op Hallo openbare multitenant-service, configureren aangepaste hostnamen voor afzonderlijke apps. Ze kunnen ook unieke SNI-SSL-certificaatbindingen voor afzonderlijke apps configureren.

## <a name="app-service-environment-v1"></a>App Service-omgeving v1 ##
App Service-omgeving zijn er twee versies: ASEv1 en ASEv2. Hallo voorgaande informatie is gebaseerd op ASEv2. Deze sectie ziet u verschillen tussen ASEv1 en ASEv2 Hallo.

In ASEv1 beheert u alle resources Hallo handmatig. Dat betekent onder meer Hallo-front-ends, werknemers en IP-adressen gebruikt voor SSL op basis van IP. Voordat u uw App Service-abonnement uitbreiden kunt, moet u uitschalen Hallo werknemersgroep dat u wilt dat toohost deze.

ASEv1 maakt gebruik van een andere prijscategorie model uit ASEv2. In ASEv1 betaalt u voor elke core toegewezen. Dat betekent onder meer kernen die worden gebruikt voor de front-ends of workers die werkbelastingen worden niet als host. Hallo standaardgrootte maximale schaal van een as-omgeving is in ASEv1, 55 totale hosts. Die bevat werknemers en -front-ends. Een voordeel tooASEv1 is dat deze kan worden geïmplementeerd in een klassiek virtueel netwerk en een virtueel netwerk van Resource Manager. toolearn meer informatie over ASEv1, Zie [App Service-omgeving v1 inleiding][ASEv1Intro].

Zie voor een ASEv1 toocreate met behulp van een Resource Manager-sjabloon [een v1 ILB as-omgeving maken met Resource Manager-sjabloon][ILBASEv1Template].


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
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
[ILBASEv1Template]: ../../app-service-web/app-service-app-service-environment-create-ilb-ase-resourcemanager.md

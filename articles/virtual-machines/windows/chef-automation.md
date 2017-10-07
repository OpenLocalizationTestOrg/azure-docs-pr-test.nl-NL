---
title: implementatie van de virtuele machine aaaAzure met Chef | Microsoft Docs
description: Meer informatie over hoe toouse Chef toodo geautomatiseerde implementatie van virtuele machines en configuratie op Microsoft Azure
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a>Implementatie van virtuele Azure-machine automatiseren met Chef
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Chef is een uitstekend hulpprogramma voor het leveren van automation en gewenste status configuraties.

Met de meest recente versie van de cloud-api Chef biedt naadloze integratie met Azure, zodat u Hallo mogelijkheid tooprovision en configuratiestatussen via één opdracht implementeren.

In dit artikel ik, ziet u hoe tooset van uw Chef omgeving tooprovision Azure virtuele machines en helpt u bij het maken van een beleid of 'CookBook' en het implementeren van deze cookbook tooan virtuele machine van Azure.

We begint!

## <a name="chef-basics"></a>Chef basisbeginselen
Voordat u begint, voorgesteld ik dat u Hallo basisconcepten van Chef bekijken. Er is geweldige materiaal <a href="http://www.chef.io/chef" target="_blank">hier</a> en ik het beste hebt u een snelle Lees voordat u deze stapsgewijze kennismaking. Ik zal echter Hallo basisbeginselen samenvatting voordat we aan de slag.

Hallo volgende diagram ziet u Hallo op hoog niveau Chef-architectuur.

![][2]

Chef heeft drie architectuur hoofdonderdelen: Chef-Server, Chef-Client (knooppunt) en Chef-werkstation.

Hallo Chef Server onze beheerpunt is en er zijn twee opties voor Hallo Chef-Server: een gehoste oplossing of een on-premises-oplossing. We gebruiken een gehoste oplossing.

Hallo Chef-Client is (knooppunt) Hallo-agent die zich bevindt op Hallo-servers die u beheert.

Hallo Chef-werkstation is onze beheerwerkstation waar we onze beleid maken en onze management-opdrachten uit te voeren. We Hallo uitvoeren **mes** opdracht van Hallo Chef werkstation toomanage onze infrastructuur.

Er is ook Hallo concept van 'Cookbooks' en 'Recepten'. Dit zijn effectief Hallo beleidsregels die we definiëren en tooour servers toepassen.

## <a name="preparing-hello-workstation"></a>Hallo-werkstation voorbereiden
Ten eerste kunt prep Hallo werkstation. Ik gebruik een standaard Windows-werkstation. Een directory toostore toocreate moeten we onze configuratiebestanden en cookbooks.

Eerst een map met de naam C:\chef maken.

Vervolgens maakt u een tweede directory c:\chef\cookbooks aangeroepen.

Nu moet toodownload ons Azure instellingenbestand zodat Chef met ons Azure-abonnement communiceren kan.

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
Download uw publicatie-instellingen met behulp van PowerShell Azure Hallo [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) opdracht. 

Sla Hallo bestand publicatie-instellingen in C:\chef.

## <a name="creating-a-managed-chef-account"></a>Een beheerde Chef-account maken
Aanmelden voor een gehoste Chef account [hier](https://manage.chef.io/signup).

Tijdens het aanmeldingsproces hello, kunt u zich toocreate gevraagd een nieuwe organisatie.

![][3]

Nadat uw organisatie is gemaakt, downloadt u Hallo starterskit.

![][4]

> [!NOTE]
> Als u gevraagd waarschuwing wordt dat uw sleutels worden opnieuw ingesteld, is ok tooproceed omdat er geen bestaande infrastructuur nog geconfigureerd.
> 
> 

Deze starter kit zip-bestand bevat de configuratiebestanden van de organisatie en de sleutels.

## <a name="configuring-hello-chef-workstation"></a>Hallo Chef werkstation configureren
Hallo-inhoud van het Hallo chef starter.zip tooC:\chef extraheren.

Kopieer alle bestanden onder chef-starter\chef-opslagplaats\.chef tooyour c:\chef directory.

Uw directory ziet er ongeveer als volgt Hallo nu.

![][5]

U hebt nu vier bestanden met inbegrip van hello Azure publishing bestand in de hoofdmap Hallo van c:\chef.

Hallo PEM-bestanden bevatten van uw organisatie en persoonlijke sleutels van de beheerder voor communicatie terwijl Hallo knife.rb bestand de configuratie van uw mes bevat. Moeten we tooedit hello knife.rb bestand.

Hallo-bestand openen in uw editor naar keuze en Hallo 'cookbook_path' wijzigen door het verwijderen van Hallo /... / van Hallo pad zodat deze wordt weergegeven zoals volgende.

    cookbook_path  ["#{current_dir}/cookbooks"]

Ook toevoegen Hallo volgende regel reflecterende Hallo-naam van uw Azure bestand publicatie-instellingen.

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

Uw knife.rb-bestand ziet er nu vergelijkbare toohello voorbeeld te volgen.

![][6]

Deze regels zorgt ervoor dat mes verwijst naar Hallo cookbooks map onder c:\chef\cookbooks en ook onze Azure Publish Settings-bestand tijdens de Azure-bewerkingen gebruikt.

## <a name="installing-hello-chef-development-kit"></a>Hallo Chef Development Kit installeren
Volgende [downloaden en installeren](http://downloads.getchef.com/chef-dk/windows) Hallo tooset uw werkstation Chef ChefDK (Chef Development Kit).

![][7]

In de standaardlocatie Hallo van c:\opscode installeren. Deze installatie duurt ongeveer 10 minuten.

Bevestig dat uw padvariabele bevat vermeldingen voor C:\opscode\chefdk\bin; C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin

Als ze niet er zijn, zorg er dan voor dat u deze paden toevoegt.

*Houd er rekening mee Hallo volgorde van de Hallo pad IS belangrijk!* Als uw opscode-paden niet in de juiste volgorde Hallo zijn hebt u problemen.

Start opnieuw op uw werkstation voordat u doorgaat.

Vervolgens installeert we Hallo mes Azure-extensie. Dit biedt mes Hallo 'Azure invoegtoepassing'.

Hallo volgende opdracht worden uitgevoerd.

    chef gem install knife-azure ––pre

> [!NOTE]
> Hallo – pre-argument zorgt ervoor dat u ontvangt Hallo nieuwste RC-versie van Hallo mes Azure invoegtoepassing waarmee toegang toohello meest recente set API's.
> 
> 

Is het waarschijnlijk dat een aantal afhankelijkheden ook worden geïnstalleerd op Hallo hetzelfde moment.

![][8]

tooensure die alles is geconfigureerd, Voer Hallo na de opdracht.

    knife azure image list

Als alles correct is geconfigureerd, ziet u een lijst met beschikbare Azure installatiekopieën door te bladeren.

Gefeliciteerd. Hallo-werkstation is ingesteld.

## <a name="creating-a-cookbook"></a>Maken van een Cookbook
Een Cookbook wordt gebruikt door Chef toodefine een reeks opdrachten die u wilt dat tooexecute op uw beheerde client. Het maken van een Cookbook is eenvoudig en gebruiken we Hallo **chef genereren cookbook** opdracht toogenerate onze Cookbook-sjabloon. Ik zal worden aanroepen van mijn webserver Cookbook als ik een beleid dat automatisch wordt geïmplementeerd IIS zou willen.

In de map C:\Chef Hallo volgende opdracht worden uitgevoerd.

    chef generate cookbook webserver

Hierdoor wordt een reeks van bestanden onder Hallo directory C:\Chef\cookbooks\webserver gegenereerd. Nu moet toodefine Hallo reeks opdrachten dat willen we graag onze client Chef tooexecute op onze beheerde virtuele machine.

Hallo-opdrachten worden opgeslagen in Hallo bestand default.rb. In dit bestand moet ik een verzameling opdrachten die IIS is geïnstalleerd, start IIS en een sjabloon toohello wwwroot-map kopieert definiëren.

Hallo C:\chef\cookbooks\webserver\recipes\default.rb bestand wijzigen en Hallo volgende regels toevoegen.

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

Hallo-bestand opslaan als u klaar bent.

## <a name="creating-a-template"></a>Maken van een sjabloon
Zoals we eerder vermeld, moet een sjabloonbestand dat wordt gebruikt als onze pagina met default.html toogenerate.

Hallo na de opdracht toogenerate Hallo sjabloon worden uitgevoerd.

    chef generate template webserver Default.htm

Ga nu toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb bestand. Hallo-bestand bewerken door enkele eenvoudige 'Hallo wereld' HTML-code toe te voegen en sla Hallo-bestand.

## <a name="upload-hello-cookbook-toohello-chef-server"></a>Hallo Cookbook toohello Chef Server uploaden
We zijn in deze stap duurt een kopie van Hallo Cookbook die er op de lokale computer gemaakt en toohello Chef gehoste Server uploaden. Na het uploaden Hallo Cookbook wordt weergegeven onder Hallo **beleid** tabblad.

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a>Een virtuele machine met Mes Azure implementeren
We nu implementeren van een virtuele machine van Azure en toepassing hello 'Webserver' Cookbook die onze IIS web service en de standaard webpagina wordt geïnstalleerd.

In volgorde van toodo dit, gebruikt u Hallo **mes azure-server maken** opdracht.

Ben voorbeeld van de opdracht Hallo volgende verschijnt.

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

Hallo parameters behoeven geen uitleg. Vervangen door uw specifieke variabelen en uitgevoerd.

> [!NOTE]
> Via Hallo Hallo-opdrachtregel, ben ik mijn filterregels voor eindpunt netwerk ook automatiseren met behulp van Hallo – tcp-eindpunten parameter. Ik hebt poorten 80 en 3389 tooprovide toegang toomy webpagina en RDP-sessie geopend.
> 
> 

Zodra u Hallo-opdracht uitvoert, gaat u toohello Azure portal en u ziet uw machine tooprovision begint.

![][13]

Hallo-opdrachtprompt verschijnt volgende.

![][10]

Zodra het Hallo-implementatie is voltooid, moet we kunnen tooconnect toohello web-service via poort 80 we had Hallo poort geopend wanneer we Hallo virtuele machine met de Hallo mes Azure opdracht ingericht. Als deze virtuele machine Hallo virtuele machine die alleen in mijn cloudservice is, moet ik het verbinding maken met Hallo cloud service-url.

![][11]

Zoals u ziet, krijg ik creative met mijn HTML-code.

Vergeet niet dat we kunnen ook verbinding maken via een RDP-sessie vanaf hello Azure-portal via poort 3389.

Ik hopen dat u dat dit is handig zijn. Ga en uw infrastructuur vandaag starten als code reis met Azure.

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->

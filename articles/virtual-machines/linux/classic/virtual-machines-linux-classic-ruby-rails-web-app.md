---
title: aaaHost Ruby op Rails website op een Linux-VM | Microsoft Docs
description: Instellen en een Ruby op Rails gebaseerde website op Azure met behulp van een virtuele Linux-machine host.
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a>Ruby on Rails-webtoepassing op een Azure VM
Deze zelfstudie laat zien hoe toohost Ruby op Rails website op Azure met behulp van een virtuele Linux-machine.  

Deze zelfstudie is gevalideerd met behulp van Ubuntu Server 14.04 TNS. Als u een ander Linux-distributiepunt gebruikt, moet u mogelijk toomodify hello tooinstall Rails stappen.

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../../../azure-resource-manager/resource-manager-deployment-model.md).  In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.
>
>

## <a name="create-an-azure-vm"></a>Een Azure virtuele machine maken
Begint met het maken van een virtuele machine in Azure met een Linux-installatiekopie.

toocreate Hallo VM, kunt u hello Azure-portal gebruiken of hello Azure-opdrachtregelinterface (CLI).

### <a name="azure-portal"></a>Azure Portal
1. Meld u aan bij Hallo [Azure-portal](https://portal.azure.com)
2. Klik op **nieuw**, typt u 'Ubuntu Server 14.04' in het zoekvak Hallo. Klik op Hallo item dat is geretourneerd door Hallo zoeken. Hallo-implementatiemodel, selecteert u **klassieke**, klik op 'Maken'.
3. Hallo basisbeginselen blade voor Hallo vereist velden waarden opgeven: naam (voor Hallo VM), gebruikersnaam, verificatietype en bijbehorende aanmeldingsreferenties hello, Azure-abonnement, resourcegroep en locatie.

   ![Maak een nieuwe Ubuntu-afbeelding](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. Nadat het Hallo VM is ingericht, klikt u op de naam van de VM Hallo en klikt u op **eindpunten** in Hallo **instellingen** categorie. Hallo SSH-eindpunt, die worden vermeld onder vinden **zelfstandige**.

   ![Standaardeindpunt](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a>Azure CLI
Volg de stappen Hallo in [maken van een virtuele Machine waarop Linux][vm-instructions].

Nadat het Hallo VM is ingericht, kunt u Hallo SSH eindpunt opvragen door het uitvoeren van de volgende opdracht Hallo:

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a>Ruby op Rails installeren
1. Gebruik SSH tooconnect toohello VM.
2. Gebruik vanaf Hallo SSH-sessie, Hallo opdrachten tooinstall Ruby op Hallo VM te volgen:

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    Hallo-installatie kan enkele minuten duren. Wanneer deze is voltooid, gebruikt u Hallo na de opdracht tooverify dat Ruby is geïnstalleerd:

        ruby -v

3. Gebruik Hallo volgende opdracht tooinstall Rails:

        sudo gem install rails --no-rdoc --no-ri -V

    Gebruik Hallo--er is geen rdoc en--Nee k vlaggen tooskip Hallo-documentatie, wat sneller is geïnstalleerd.
    Met deze opdracht wordt waarschijnlijk lang duren tooexecute, zodat toe te voegen Hallo -V wordt informatie over Hallo installatievoortgang weergegeven.

## <a name="create-and-run-an-app"></a>Maken en een app uitvoeren
Terwijl u nog steeds wordt aangemeld via SSH, voert u Hallo volgende opdrachten:

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

Hallo [nieuwe](http://guides.rubyonrails.org/command_line.html#rails-new) opdracht maakt u een nieuwe Rails-app. Hallo [server](http://guides.rubyonrails.org/command_line.html#rails-server) opdracht start Hallo WEBrick-webserver die wordt geleverd met Rails. (Voor gebruik in productieomgevingen, zou wilt u waarschijnlijk een andere server, zoals Eenhoorn of passagiers toouse.)

Hier ziet u uitvoer vergelijkbare toohello volgende.

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a>Een eindpunt toevoegen
1. Ga toohello [Azure portal] [https://portal.azure.com] en selecteert u de virtuele machine.

2. Selecteer **EINDPUNTEN** in Hallo **instellingen** langs Hallo linkerrand Hallo pagina.

3. Klik op **toevoegen** bovenaan Hallo Hallo pagina.

4. In Hallo **eindpunt toevoegen** dialoogvenster pagina, voert u Hallo volgende informatie:

   * **Naam**: HTTP
   * **Protocol**: TCP
   * **Openbare poort**: 80
   * **Particuliere poort**: 3000
   * **Zwevende PI adres**: uitgeschakeld
   * **ACL - volgorde**: 1001 of een andere waarde die Hallo prioriteit van deze regel wordt ingesteld.
   * **ACL - naam**: allowHTTP
   * **ACL - actie**: toestaan
   * **ACL - extern subnet**: 1.0.0.0/16

     Dit eindpunt heeft een openbare poort 80 die netwerkverkeer toohello particuliere poort 3000 routeert, waarbij Hallo Rails server luistert. Hallo toegangsbeheerlijstregel kunt openbaar verkeer op poort 80.

     ![nieuwe endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. Klik op OK toosave Hallo-eindpunt.

6. Een bericht moet worden weergegeven waarin wordt vermeld **eindpunt van de virtuele machine opslaan**. Als dit bericht verdwijnt, is Hallo eindpunt actief. U kunt nu uw toepassing testen door te navigeren toohello DNS-naam van uw virtuele machine. Hallo-website moet vergelijkbaar toohello volgende weergegeven:

    ![standaardpagina rails][default-rails-cloud]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u de meeste Hallo stappen handmatig. In een productieomgeving zou u uw app op een ontwikkelcomputer schrijven en implementeert u deze toohello Azure VM. Ook hosttoepassing de meeste productieomgevingen Hallo Rails in combinatie met een andere server-proces zoals Apache of NginX, welke ingangen aanvragen routering toomultiple exemplaren van Hallo Rails toepassing ten behoeve van statische resources. Zie http://rubyonrails.org/deploy/ voor meer informatie.

toolearn meer informatie over Ruby op Rails, gaat u naar Hallo [Ruby op Rails handleidingen][rails-guides].

toouse Azure services van uw toepassing Ruby, Zie:

* [Niet-gestructureerde gegevens blobs opslaan][blobs]
* [Store sleutel-waardeparen met tabellen][tables]
* [Hoge bandbreedte inhoud leveren met Hallo inhoud Delivery Network][cdn-howto]

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png

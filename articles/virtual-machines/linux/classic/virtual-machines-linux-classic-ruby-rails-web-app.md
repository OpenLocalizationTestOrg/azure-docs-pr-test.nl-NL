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
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="7bbd5-103">Ruby on Rails-webtoepassing op een Azure VM</span><span class="sxs-lookup"><span data-stu-id="7bbd5-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="7bbd5-104">Deze zelfstudie laat zien hoe toohost Ruby op Rails website op Azure met behulp van een virtuele Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-104">This tutorial shows how toohost a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="7bbd5-105">Deze zelfstudie is gevalideerd met behulp van Ubuntu Server 14.04 TNS.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="7bbd5-106">Als u een ander Linux-distributiepunt gebruikt, moet u mogelijk toomodify hello tooinstall Rails stappen.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-106">If you use a different Linux distribution, you might need toomodify hello steps tooinstall Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7bbd5-107">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7bbd5-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="7bbd5-108">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="7bbd5-109">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="7bbd5-110">Een Azure virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="7bbd5-110">Create an Azure VM</span></span>
<span data-ttu-id="7bbd5-111">Begint met het maken van een virtuele machine in Azure met een Linux-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="7bbd5-112">toocreate Hallo VM, kunt u hello Azure-portal gebruiken of hello Azure-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="7bbd5-112">toocreate hello VM, you can use hello Azure portal or hello Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="7bbd5-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7bbd5-113">Azure portal</span></span>
1. <span data-ttu-id="7bbd5-114">Meld u aan bij Hallo [Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="7bbd5-114">Sign into hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="7bbd5-115">Klik op **nieuw**, typt u 'Ubuntu Server 14.04' in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-115">Click **New**, then type "Ubuntu Server 14.04" in hello search box.</span></span> <span data-ttu-id="7bbd5-116">Klik op Hallo item dat is geretourneerd door Hallo zoeken.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-116">Click hello entry returned by hello search.</span></span> <span data-ttu-id="7bbd5-117">Hallo-implementatiemodel, selecteert u **klassieke**, klik op 'Maken'.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-117">For hello deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="7bbd5-118">Hallo basisbeginselen blade voor Hallo vereist velden waarden opgeven: naam (voor Hallo VM), gebruikersnaam, verificatietype en bijbehorende aanmeldingsreferenties hello, Azure-abonnement, resourcegroep en locatie.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-118">In hello Basics blade, supply values for hello required fields: Name (for hello VM), User name, Authentication type and hello corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Maak een nieuwe Ubuntu-afbeelding](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="7bbd5-120">Nadat het Hallo VM is ingericht, klikt u op de naam van de VM Hallo en klikt u op **eindpunten** in Hallo **instellingen** categorie.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-120">After hello VM is provisioned, click on hello VM name, and click **Endpoints** in hello **Settings** category.</span></span> <span data-ttu-id="7bbd5-121">Hallo SSH-eindpunt, die worden vermeld onder vinden **zelfstandige**.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-121">Find hello SSH endpoint, listed under **Standalone**.</span></span>

   ![Standaardeindpunt](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="7bbd5-123">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7bbd5-123">Azure CLI</span></span>
<span data-ttu-id="7bbd5-124">Volg de stappen Hallo in [maken van een virtuele Machine waarop Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="7bbd5-124">Follow hello steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="7bbd5-125">Nadat het Hallo VM is ingericht, kunt u Hallo SSH eindpunt opvragen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="7bbd5-125">After hello VM is provisioned, you can get hello SSH endpoint by running hello following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="7bbd5-126">Ruby op Rails installeren</span><span class="sxs-lookup"><span data-stu-id="7bbd5-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="7bbd5-127">Gebruik SSH tooconnect toohello VM.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-127">Use SSH tooconnect toohello VM.</span></span>
2. <span data-ttu-id="7bbd5-128">Gebruik vanaf Hallo SSH-sessie, Hallo opdrachten tooinstall Ruby op Hallo VM te volgen:</span><span class="sxs-lookup"><span data-stu-id="7bbd5-128">From hello SSH session, use hello following commands tooinstall Ruby on hello VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    <span data-ttu-id="7bbd5-129">Hallo-installatie kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-129">hello installation may take a few minutes.</span></span> <span data-ttu-id="7bbd5-130">Wanneer deze is voltooid, gebruikt u Hallo na de opdracht tooverify dat Ruby is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="7bbd5-130">When it completes, use hello following command tooverify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="7bbd5-131">Gebruik Hallo volgende opdracht tooinstall Rails:</span><span class="sxs-lookup"><span data-stu-id="7bbd5-131">Use hello following command tooinstall Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="7bbd5-132">Gebruik Hallo--er is geen rdoc en--Nee k vlaggen tooskip Hallo-documentatie, wat sneller is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-132">Use hello --no-rdoc and --no-ri flags tooskip installing hello documentation, which is faster.</span></span>
    <span data-ttu-id="7bbd5-133">Met deze opdracht wordt waarschijnlijk lang duren tooexecute, zodat toe te voegen Hallo -V wordt informatie over Hallo installatievoortgang weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-133">This command will likely take a long time tooexecute, so adding hello -V will display information about hello installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="7bbd5-134">Maken en een app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7bbd5-134">Create and run an app</span></span>
<span data-ttu-id="7bbd5-135">Terwijl u nog steeds wordt aangemeld via SSH, voert u Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="7bbd5-135">While still logged in via SSH, run hello following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="7bbd5-136">Hallo [nieuwe](http://guides.rubyonrails.org/command_line.html#rails-new) opdracht maakt u een nieuwe Rails-app.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-136">hello [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="7bbd5-137">Hallo [server](http://guides.rubyonrails.org/command_line.html#rails-server) opdracht start Hallo WEBrick-webserver die wordt geleverd met Rails.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-137">hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts hello WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="7bbd5-138">(Voor gebruik in productieomgevingen, zou wilt u waarschijnlijk een andere server, zoals Eenhoorn of passagiers toouse.)</span><span class="sxs-lookup"><span data-stu-id="7bbd5-138">(For production use, you would probably want toouse a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="7bbd5-139">Hier ziet u uitvoer vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-139">You should see output similar toohello following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="7bbd5-140">Een eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="7bbd5-140">Add an endpoint</span></span>
1. <span data-ttu-id="7bbd5-141">Ga toohello [Azure portal] [https://portal.azure.com] en selecteert u de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-141">Go toohello [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="7bbd5-142">Selecteer **EINDPUNTEN** in Hallo **instellingen** langs Hallo linkerrand Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-142">Select **ENDPOINTS** in hello **Settings** along hello left edge hello page.</span></span>

3. <span data-ttu-id="7bbd5-143">Klik op **toevoegen** bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-143">Click **ADD** at hello top of hello page.</span></span>

4. <span data-ttu-id="7bbd5-144">In Hallo **eindpunt toevoegen** dialoogvenster pagina, voert u Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="7bbd5-144">In hello **Add endpoint** dialog page, enter hello following information:</span></span>

   * <span data-ttu-id="7bbd5-145">**Naam**: HTTP</span><span class="sxs-lookup"><span data-stu-id="7bbd5-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="7bbd5-146">**Protocol**: TCP</span><span class="sxs-lookup"><span data-stu-id="7bbd5-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="7bbd5-147">**Openbare poort**: 80</span><span class="sxs-lookup"><span data-stu-id="7bbd5-147">**Public port**: 80</span></span>
   * <span data-ttu-id="7bbd5-148">**Particuliere poort**: 3000</span><span class="sxs-lookup"><span data-stu-id="7bbd5-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="7bbd5-149">**Zwevende PI adres**: uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="7bbd5-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="7bbd5-150">**ACL - volgorde**: 1001 of een andere waarde die Hallo prioriteit van deze regel wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-150">**Access control list - Order**: 1001, or another value that sets hello priority of this access rule.</span></span>
   * <span data-ttu-id="7bbd5-151">**ACL - naam**: allowHTTP</span><span class="sxs-lookup"><span data-stu-id="7bbd5-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="7bbd5-152">**ACL - actie**: toestaan</span><span class="sxs-lookup"><span data-stu-id="7bbd5-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="7bbd5-153">**ACL - extern subnet**: 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="7bbd5-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="7bbd5-154">Dit eindpunt heeft een openbare poort 80 die netwerkverkeer toohello particuliere poort 3000 routeert, waarbij Hallo Rails server luistert.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-154">This endpoint  has a public port of 80 that will route traffic toohello private port of 3000, where hello Rails server is listening.</span></span> <span data-ttu-id="7bbd5-155">Hallo toegangsbeheerlijstregel kunt openbaar verkeer op poort 80.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-155">hello access control list rule allows public traffic on port 80.</span></span>

     ![nieuwe endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="7bbd5-157">Klik op OK toosave Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-157">Click OK toosave hello endpoint.</span></span>

6. <span data-ttu-id="7bbd5-158">Een bericht moet worden weergegeven waarin wordt vermeld **eindpunt van de virtuele machine opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="7bbd5-159">Als dit bericht verdwijnt, is Hallo eindpunt actief.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-159">Once this message disappears, hello endpoint is active.</span></span> <span data-ttu-id="7bbd5-160">U kunt nu uw toepassing testen door te navigeren toohello DNS-naam van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-160">You may now test your application by navigating toohello DNS name of your virtual machine.</span></span> <span data-ttu-id="7bbd5-161">Hallo-website moet vergelijkbaar toohello volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7bbd5-161">hello website should appear similar toohello following:</span></span>

    ![standaardpagina rails][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="7bbd5-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7bbd5-163">Next steps</span></span>
<span data-ttu-id="7bbd5-164">In deze zelfstudie hebt u de meeste Hallo stappen handmatig.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-164">In this tutorial, you did most of hello steps manually.</span></span> <span data-ttu-id="7bbd5-165">In een productieomgeving zou u uw app op een ontwikkelcomputer schrijven en implementeert u deze toohello Azure VM.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-165">In a production environment, you would write your app on a development machine and deploy it toohello Azure VM.</span></span> <span data-ttu-id="7bbd5-166">Ook hosttoepassing de meeste productieomgevingen Hallo Rails in combinatie met een andere server-proces zoals Apache of NginX, welke ingangen aanvragen routering toomultiple exemplaren van Hallo Rails toepassing ten behoeve van statische resources.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-166">Also, most production environments host hello Rails application in conjunction with another server process such as Apache or NginX, which handles request routing toomultiple instances of hello Rails application and serving static resources.</span></span> <span data-ttu-id="7bbd5-167">Zie http://rubyonrails.org/deploy/ voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7bbd5-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="7bbd5-168">toolearn meer informatie over Ruby op Rails, gaat u naar Hallo [Ruby op Rails handleidingen][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="7bbd5-168">toolearn more about Ruby on Rails, visit hello [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="7bbd5-169">toouse Azure services van uw toepassing Ruby, Zie:</span><span class="sxs-lookup"><span data-stu-id="7bbd5-169">toouse Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="7bbd5-170">[Niet-gestructureerde gegevens blobs opslaan][blobs]</span><span class="sxs-lookup"><span data-stu-id="7bbd5-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="7bbd5-171">[Store sleutel-waardeparen met tabellen][tables]</span><span class="sxs-lookup"><span data-stu-id="7bbd5-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="7bbd5-172">[Hoge bandbreedte inhoud leveren met Hallo inhoud Delivery Network][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="7bbd5-172">[Serve high bandwidth content with hello Content Delivery Network][cdn-howto]</span></span>

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

---
title: Een Ruby op Rails website op een Linux-VM hosten | Microsoft Docs
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
ms.openlocfilehash: 0518519da6c5e62a863a47d6743ab7b7c5923acf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="5a76b-103">Ruby on Rails-webtoepassing op een Azure VM</span><span class="sxs-lookup"><span data-stu-id="5a76b-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="5a76b-104">Deze zelfstudie laat zien hoe voor het hosten van een Ruby op Rails website op Azure met behulp van een virtuele Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="5a76b-104">This tutorial shows how to host a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="5a76b-105">Deze zelfstudie is gevalideerd met behulp van Ubuntu Server 14.04 TNS.</span><span class="sxs-lookup"><span data-stu-id="5a76b-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="5a76b-106">Als u een ander Linux-distributiepunt gebruikt, moet u mogelijk de stappen voor het installeren van Rails wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5a76b-106">If you use a different Linux distribution, you might need to modify the steps to install Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a76b-107">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5a76b-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="5a76b-108">Dit artikel gaat over het gebruik van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="5a76b-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="5a76b-109">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5a76b-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="5a76b-110">Een Azure virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="5a76b-110">Create an Azure VM</span></span>
<span data-ttu-id="5a76b-111">Begint met het maken van een virtuele machine in Azure met een Linux-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="5a76b-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="5a76b-112">U kunt de Azure portal of de Azure-opdrachtregelinterface (CLI) gebruiken voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5a76b-112">To create the VM, you can use the Azure portal or the Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="5a76b-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5a76b-113">Azure portal</span></span>
1. <span data-ttu-id="5a76b-114">Meld u aan bij de [Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="5a76b-114">Sign into the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="5a76b-115">Klik op **nieuw**, typt u 'Ubuntu Server 14.04' in het zoekvak.</span><span class="sxs-lookup"><span data-stu-id="5a76b-115">Click **New**, then type "Ubuntu Server 14.04" in the search box.</span></span> <span data-ttu-id="5a76b-116">Klik op het item dat is geretourneerd door de zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="5a76b-116">Click the entry returned by the search.</span></span> <span data-ttu-id="5a76b-117">Selecteer het implementatiemodel **klassieke**, klik op 'Maken'.</span><span class="sxs-lookup"><span data-stu-id="5a76b-117">For the deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="5a76b-118">Geef waarden voor de vereiste velden in de blade grondbeginselen: naam (voor de virtuele machine), gebruikersnaam, authenticatietype en de bijbehorende aanmeldingsreferenties Azure-abonnement, resourcegroep en locatie.</span><span class="sxs-lookup"><span data-stu-id="5a76b-118">In the Basics blade, supply values for the required fields: Name (for the VM), User name, Authentication type and the corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Maak een nieuwe Ubuntu-afbeelding](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="5a76b-120">Nadat de virtuele machine is ingericht, klik op de VM-naam en klikt u op **eindpunten** in de **instellingen** categorie.</span><span class="sxs-lookup"><span data-stu-id="5a76b-120">After the VM is provisioned, click on the VM name, and click **Endpoints** in the **Settings** category.</span></span> <span data-ttu-id="5a76b-121">De SSH-eindpunt, die worden vermeld onder vinden **zelfstandige**.</span><span class="sxs-lookup"><span data-stu-id="5a76b-121">Find the SSH endpoint, listed under **Standalone**.</span></span>

   ![Standaardeindpunt](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="5a76b-123">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5a76b-123">Azure CLI</span></span>
<span data-ttu-id="5a76b-124">Volg de stappen in [maken van een virtuele Machine waarop Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="5a76b-124">Follow the steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="5a76b-125">Nadat de virtuele machine is ingericht, kunt u het SSH-eindpunt kunt krijgen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5a76b-125">After the VM is provisioned, you can get the SSH endpoint by running the following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="5a76b-126">Ruby op Rails installeren</span><span class="sxs-lookup"><span data-stu-id="5a76b-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="5a76b-127">SSH gebruiken voor verbinding met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5a76b-127">Use SSH to connect to the VM.</span></span>
2. <span data-ttu-id="5a76b-128">Gebruik de volgende opdrachten Ruby installeren op de virtuele machine van de SSH-sessie:</span><span class="sxs-lookup"><span data-stu-id="5a76b-128">From the SSH session, use the following commands to install Ruby on the VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > The brightbox repository contains the current Ruby distribution.

    <span data-ttu-id="5a76b-129">De installatie kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="5a76b-129">The installation may take a few minutes.</span></span> <span data-ttu-id="5a76b-130">Wanneer deze is voltooid, moet u de volgende opdracht gebruiken om te controleren of Ruby is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="5a76b-130">When it completes, use the following command to verify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="5a76b-131">Gebruik de volgende opdracht voor het installeren van Rails:</span><span class="sxs-lookup"><span data-stu-id="5a76b-131">Use the following command to install Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="5a76b-132">Gebruik de--vlaggen Nee rdoc en--Nee k om over te slaan voor het installeren van de documentatie, die sneller is.</span><span class="sxs-lookup"><span data-stu-id="5a76b-132">Use the --no-rdoc and --no-ri flags to skip installing the documentation, which is faster.</span></span>
    <span data-ttu-id="5a76b-133">Met deze opdracht wordt waarschijnlijk lang duren om uit te voeren, zodat de -V toe te voegen, wordt informatie over de installatievoortgang weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5a76b-133">This command will likely take a long time to execute, so adding the -V will display information about the installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="5a76b-134">Maken en een app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5a76b-134">Create and run an app</span></span>
<span data-ttu-id="5a76b-135">Terwijl u nog steeds wordt aangemeld via SSH, voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="5a76b-135">While still logged in via SSH, run the following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="5a76b-136">De [nieuwe](http://guides.rubyonrails.org/command_line.html#rails-new) opdracht maakt u een nieuwe Rails-app.</span><span class="sxs-lookup"><span data-stu-id="5a76b-136">The [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="5a76b-137">De [server](http://guides.rubyonrails.org/command_line.html#rails-server) opdracht start u de webserver WEBrick die wordt geleverd met Rails.</span><span class="sxs-lookup"><span data-stu-id="5a76b-137">The [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts the WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="5a76b-138">(Voor gebruik in productieomgevingen, u wilt waarschijnlijk wilt gebruiken een andere server, zoals Eenhoorn of passagiers.)</span><span class="sxs-lookup"><span data-stu-id="5a76b-138">(For production use, you would probably want to use a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="5a76b-139">De uitvoer ziet er als volgt uit.</span><span class="sxs-lookup"><span data-stu-id="5a76b-139">You should see output similar to the following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C to shutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="5a76b-140">Een eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="5a76b-140">Add an endpoint</span></span>
1. <span data-ttu-id="5a76b-141">Ga naar de [Azure portal] [https://portal.azure.com] en selecteert u de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5a76b-141">Go to the [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="5a76b-142">Selecteer **EINDPUNTEN** in de **instellingen** langs de linkerkant van de rand de pagina.</span><span class="sxs-lookup"><span data-stu-id="5a76b-142">Select **ENDPOINTS** in the **Settings** along the left edge the page.</span></span>

3. <span data-ttu-id="5a76b-143">Klik op **toevoegen** boven aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="5a76b-143">Click **ADD** at the top of the page.</span></span>

4. <span data-ttu-id="5a76b-144">In de **eindpunt toevoegen** dialoogvenster pagina, voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="5a76b-144">In the **Add endpoint** dialog page, enter the following information:</span></span>

   * <span data-ttu-id="5a76b-145">**Naam**: HTTP</span><span class="sxs-lookup"><span data-stu-id="5a76b-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="5a76b-146">**Protocol**: TCP</span><span class="sxs-lookup"><span data-stu-id="5a76b-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="5a76b-147">**Openbare poort**: 80</span><span class="sxs-lookup"><span data-stu-id="5a76b-147">**Public port**: 80</span></span>
   * <span data-ttu-id="5a76b-148">**Particuliere poort**: 3000</span><span class="sxs-lookup"><span data-stu-id="5a76b-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="5a76b-149">**Zwevende PI adres**: uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="5a76b-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="5a76b-150">**ACL - volgorde**: 1001 of een andere waarde die de prioriteit van deze regel wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5a76b-150">**Access control list - Order**: 1001, or another value that sets the priority of this access rule.</span></span>
   * <span data-ttu-id="5a76b-151">**ACL - naam**: allowHTTP</span><span class="sxs-lookup"><span data-stu-id="5a76b-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="5a76b-152">**ACL - actie**: toestaan</span><span class="sxs-lookup"><span data-stu-id="5a76b-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="5a76b-153">**ACL - extern subnet**: 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5a76b-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="5a76b-154">Dit eindpunt heeft een openbare poort 80 dat verkeer wordt gerouteerd naar de particuliere poort van 3000, waarbij de Rails server luistert.</span><span class="sxs-lookup"><span data-stu-id="5a76b-154">This endpoint  has a public port of 80 that will route traffic to the private port of 3000, where the Rails server is listening.</span></span> <span data-ttu-id="5a76b-155">De toegangsbeheerlijstregel kunt openbaar verkeer op poort 80.</span><span class="sxs-lookup"><span data-stu-id="5a76b-155">The access control list rule allows public traffic on port 80.</span></span>

     ![nieuwe endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="5a76b-157">Klik op OK om op te slaan van het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="5a76b-157">Click OK to save the endpoint.</span></span>

6. <span data-ttu-id="5a76b-158">Een bericht moet worden weergegeven waarin wordt vermeld **eindpunt van de virtuele machine opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5a76b-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="5a76b-159">Als dit bericht verdwijnt, is het eindpunt is actief.</span><span class="sxs-lookup"><span data-stu-id="5a76b-159">Once this message disappears, the endpoint is active.</span></span> <span data-ttu-id="5a76b-160">U kunt nu uw toepassing testen door te navigeren naar de DNS-naam van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5a76b-160">You may now test your application by navigating to the DNS name of your virtual machine.</span></span> <span data-ttu-id="5a76b-161">De website moet worden de volgende strekking weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5a76b-161">The website should appear similar to the following:</span></span>

    ![standaardpagina rails][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="5a76b-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a76b-163">Next steps</span></span>
<span data-ttu-id="5a76b-164">In deze zelfstudie hebt u de meeste van de stappen handmatig.</span><span class="sxs-lookup"><span data-stu-id="5a76b-164">In this tutorial, you did most of the steps manually.</span></span> <span data-ttu-id="5a76b-165">In een productieomgeving zou u uw app op een ontwikkelcomputer schrijven en deze implementeren in de Azure VM.</span><span class="sxs-lookup"><span data-stu-id="5a76b-165">In a production environment, you would write your app on a development machine and deploy it to the Azure VM.</span></span> <span data-ttu-id="5a76b-166">De meeste productieomgevingen hosten ook de toepassing Rails in combinatie met een andere server-proces zoals Apache of NginX, welke ingangen aanvragen routering naar meerdere exemplaren van de toepassing Rails ten behoeve van statische resources.</span><span class="sxs-lookup"><span data-stu-id="5a76b-166">Also, most production environments host the Rails application in conjunction with another server process such as Apache or NginX, which handles request routing to multiple instances of the Rails application and serving static resources.</span></span> <span data-ttu-id="5a76b-167">Zie http://rubyonrails.org/deploy/ voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5a76b-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="5a76b-168">Voor meer informatie over Ruby op Rails, gaat u naar de [Ruby op Rails handleidingen][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="5a76b-168">To learn more about Ruby on Rails, visit the [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="5a76b-169">Voor het gebruik van Azure-services van uw toepassing Ruby, Zie:</span><span class="sxs-lookup"><span data-stu-id="5a76b-169">To use Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="5a76b-170">[Niet-gestructureerde gegevens blobs opslaan][blobs]</span><span class="sxs-lookup"><span data-stu-id="5a76b-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="5a76b-171">[Store sleutel-waardeparen met tabellen][tables]</span><span class="sxs-lookup"><span data-stu-id="5a76b-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="5a76b-172">[Inhoud van de hoge bandbreedte met het netwerk van de levering van inhoud][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="5a76b-172">[Serve high bandwidth content with the Content Delivery Network][cdn-howto]</span></span>

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

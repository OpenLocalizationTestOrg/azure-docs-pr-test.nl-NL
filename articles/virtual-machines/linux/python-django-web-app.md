---
title: web-app met Django op een Azure Linux VM aaaPython | Microsoft Docs
description: Meer informatie over hoe toohost een Django-gebaseerde web-app in Azure met behulp van een Linux-VM.
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="25088-103">Django Hallo wereld-web-app op een Linux-VM</span><span class="sxs-lookup"><span data-stu-id="25088-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="25088-104">Windows</span><span class="sxs-lookup"><span data-stu-id="25088-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="25088-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="25088-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="25088-106">Deze zelfstudie leert u hoe toohost een website op basis van Django in Linux in Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="25088-106">This tutorial shows you how toohost a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="25088-107">In de zelfstudie Hallo we ervan uitgaan dat geen ervaring met Azure.</span><span class="sxs-lookup"><span data-stu-id="25088-107">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="25088-108">Wanneer u Hallo-zelfstudie hebt voltooid, hebt u een Django-toepassing up en wordt uitgevoerd in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="25088-108">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="25088-109">Leer hoe u het volgende doet:</span><span class="sxs-lookup"><span data-stu-id="25088-109">Learn how to:</span></span>

* <span data-ttu-id="25088-110">Instellen van een virtuele machine van Azure toohost Django.</span><span class="sxs-lookup"><span data-stu-id="25088-110">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="25088-111">Hoewel deze zelfstudie wordt uitgelegd hoe toodo dit voor **Linux**, kunt u doen hello dezelfde voor een Windows Server-VM gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="25088-111">Although this tutorial explains how toodo this for **Linux**, you can do hello same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="25088-112">Een nieuwe Django-toepassing maken in Linux.</span><span class="sxs-lookup"><span data-stu-id="25088-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="25088-113">Hallo-zelfstudie laat zien hoe toobuild een basic Hallo wereld-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="25088-113">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="25088-114">Hallo-toepassing wordt gehost in Azure een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="25088-114">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="25088-115">Hallo volgende schermafbeelding ziet u de toepassing hello voltooid:</span><span class="sxs-lookup"><span data-stu-id="25088-115">hello following screenshot shows hello completed application:</span></span>

![Hallo Hallo wereld-pagina in een browservenster wordt weergegeven in Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="25088-117">Maken en een virtuele machine van Azure toohost Django instellen</span><span class="sxs-lookup"><span data-stu-id="25088-117">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="25088-118">toocreate een virtuele machine van Azure met Hallo Ubuntu Server 14.04 TNS distributie, Zie [virtuele Linux-machine maken in Azure-portal Hallo](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="25088-118">toocreate an Azure virtual machine with hello Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in hello Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="25088-119">U kunt ook wachtwoordverificatie in plaats van een openbare SSH-sleutel.</span><span class="sxs-lookup"><span data-stu-id="25088-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="25088-120">tooedit hello network security groep tooallow binnenkomende HTTP-verkeer tooport 80, Zie [netwerkbeveiligingsgroepen maken in Azure-portal Hallo](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="25088-120">tooedit hello network security group tooallow incoming HTTP traffic tooport 80, see [Create network security groups in hello Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="25088-121">(Optioneel) Uw nieuwe virtuele machine geen standaard een volledig gekwalificeerde domeinnaam (FQDN).</span><span class="sxs-lookup"><span data-stu-id="25088-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="25088-122">een virtuele machine met een FQDN toocreate Zie [maken van een FQDN-naam in hello Azure-portal voor een virtuele machine van Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="25088-122">toocreate a VM with an FQDN, see [Create an FQDN in hello Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="25088-123">Deze stap is niet vereist voor het voltooien van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="25088-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="25088-124"><a id="setup"></a>Hello ontwikkelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="25088-124"><a id="setup"> </a>Set up hello development environment</span></span>
> [!NOTE]
> <span data-ttu-id="25088-125">Als u Python tooinstall moet of toouse Hallo clientbibliotheken wilt, raadpleegt u Hallo [Python installatiehandleiding](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="25088-125">If you need tooinstall Python or want toouse hello client libraries, see hello [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="25088-126">Hallo Ubuntu Linux VM heeft Python 2.7 vooraf geïnstalleerd, maar deze wordt niet geleverd met Apache of Django.</span><span class="sxs-lookup"><span data-stu-id="25088-126">hello Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="25088-127">Volgende stappen tooconnect tooyour VM Hallo voltooien en Apache en Django te installeren:</span><span class="sxs-lookup"><span data-stu-id="25088-127">Complete hello following steps tooconnect tooyour VM and install Apache and Django:</span></span>

1. <span data-ttu-id="25088-128">Open een nieuw venster van de Terminal.</span><span class="sxs-lookup"><span data-stu-id="25088-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="25088-129">tooconnect toohello Azure virtuele machine, Voer Hallo na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="25088-129">tooconnect toohello Azure VM, enter hello following command.</span></span> <span data-ttu-id="25088-130">Als u een FQDN-naam hebt gemaakt, kunt u verbinding maken met behulp van het openbare IP-adres hello, die wordt weergegeven in de Hallo virtuele machine samenvatting in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="25088-130">If you didn't create an FQDN, you can connect by using hello public IP address that's displayed in hello virtual machine summary in hello Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="25088-131">tooinstall Django, Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="25088-131">tooinstall Django, enter hello following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="25088-132">tooinstall Apache met rest-wsgi Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="25088-132">tooinstall Apache with mod-wsgi, enter hello following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="25088-133">Een nieuwe Django-app maken</span><span class="sxs-lookup"><span data-stu-id="25088-133">Create a new Django app</span></span>
1. <span data-ttu-id="25088-134">toouse SSH tooaccess uw VM, open Hallo terminalvenster u in de voorgaande sectie Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="25088-134">toouse SSH tooaccess your VM, open hello Terminal window you used in hello preceding section.</span></span>
2. <span data-ttu-id="25088-135">toocreate een nieuwe Django-project, geef Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="25088-135">toocreate a new Django project, enter hello following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="25088-136">Hallo `django-admin.py` script genereert een basisstructuur voor Django-gebaseerde websites:</span><span class="sxs-lookup"><span data-stu-id="25088-136">hello `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="25088-137">`helloworld/manage.py`helpt u te hosten en stoppen met het hosten van uw website op basis van een Django.</span><span class="sxs-lookup"><span data-stu-id="25088-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="25088-138">`helloworld/helloworld/settings.py`Django-instellingen voor de toepassing is.</span><span class="sxs-lookup"><span data-stu-id="25088-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="25088-139">`helloworld/helloworld/urls.py`heeft Hallo toewijzing code tussen elke URL en de weergave.</span><span class="sxs-lookup"><span data-stu-id="25088-139">`helloworld/helloworld/urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="25088-140">In Hallo /var/www/helloworld/helloworld directory, maakt u een nieuw bestand met de naam views.py.</span><span class="sxs-lookup"><span data-stu-id="25088-140">In hello /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="25088-141">Dit bestand heeft Hallo weergeven dat Hallo "Hallo wereld" pagina weergeeft.</span><span class="sxs-lookup"><span data-stu-id="25088-141">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="25088-142">Voer in de code-editor Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="25088-142">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="25088-143">Hallo-inhoud van Hallo urls.py bestand vervangen door Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="25088-143">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="25088-144">Apache instellen</span><span class="sxs-lookup"><span data-stu-id="25088-144">Set up Apache</span></span>
1. <span data-ttu-id="25088-145">Maak een Apache virtuele host-configuratiebestand in Hallo /etc/apache2/sites-available/helloworld.conf map.</span><span class="sxs-lookup"><span data-stu-id="25088-145">In hello /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="25088-146">Hallo inhoud toohello volgende waarden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="25088-146">Set hello contents toohello following values.</span></span> <span data-ttu-id="25088-147">Vervang *yourVmName* met Hallo werkelijke naam van de door u gebruikte computer hello (bijvoorbeeld *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="25088-147">Replace *yourVmName* with hello actual name of hello machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="25088-148">tooactivate hello site gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="25088-148">tooactivate hello site, use hello following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="25088-149">toorestart Apache Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="25088-149">toorestart Apache, use hello following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="25088-150">Hallo webpagina in uw browser worden geladen:</span><span class="sxs-lookup"><span data-stu-id="25088-150">Load hello webpage in your browser:</span></span>
   
   ![Een browservenster Hallo Hallo wereldpagina wordt weergegeven in Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="25088-152">De virtuele machine van Azure afsluiten</span><span class="sxs-lookup"><span data-stu-id="25088-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="25088-153">Wanneer u met deze zelfstudie bent klaar, wordt aangeraden u afgesloten of hello Azure VM die u hebt gemaakt voor de zelfstudie Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="25088-153">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="25088-154">Hiermee wordt vrijgemaakt bronnen voor andere zelfstudies en kunt u voorkomen dat Azure gebruikskosten aangaan.</span><span class="sxs-lookup"><span data-stu-id="25088-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>


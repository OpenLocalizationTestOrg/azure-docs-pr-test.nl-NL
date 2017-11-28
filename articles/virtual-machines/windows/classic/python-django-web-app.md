---
title: aaaDjango web-app op een Windows Server Azure VM | Microsoft Docs
description: Meer informatie over hoe een website op basis van Django in Azure met behulp van een VM van Windows Server 2012 R2 Datacenter met het klassieke implementatiemodel Hallo toohost.
services: virtual-machines-windows
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-service-management
ms.assetid: e36484d1-afbf-47f5-b755-5e65397dc1c3
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 55847e3c6d6769965be29077e8d4eeebad914637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="1587c-103">Django Hallo wereld-web-app op een virtuele machine van Windows Server</span><span class="sxs-lookup"><span data-stu-id="1587c-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="1587c-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en Hallo klassieke implementatiemodel](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1587c-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and hello classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1587c-105">Dit artikel wordt beschreven Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="1587c-105">This article describes hello classic deployment model.</span></span> <span data-ttu-id="1587c-106">U wordt aangeraden de meeste nieuwe implementaties Hallo Resource Manager-model gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1587c-106">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="1587c-107">Deze zelfstudie leert u hoe toohost een website op basis van Django in Windows Server in Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="1587c-107">This tutorial shows you how toohost a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="1587c-108">In de zelfstudie Hallo we ervan uitgaan dat geen ervaring met Azure.</span><span class="sxs-lookup"><span data-stu-id="1587c-108">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="1587c-109">Wanneer u Hallo-zelfstudie hebt voltooid, hebt u een Django-toepassing up en wordt uitgevoerd in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="1587c-109">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="1587c-110">Leer hoe u het volgende doet:</span><span class="sxs-lookup"><span data-stu-id="1587c-110">Learn how to:</span></span>

* <span data-ttu-id="1587c-111">Instellen van een virtuele machine van Azure toohost Django.</span><span class="sxs-lookup"><span data-stu-id="1587c-111">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="1587c-112">Hoewel deze zelfstudie wordt uitgelegd hoe toodo dit voor **Windows Server**, kunt u doen Hallo dezelfde voor een Linux-VM wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="1587c-112">Although this tutorial explains how toodo this for **Windows Server**, you can do hello same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="1587c-113">Maak een nieuwe Django-toepassing in Windows.</span><span class="sxs-lookup"><span data-stu-id="1587c-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="1587c-114">Hallo-zelfstudie laat zien hoe toobuild een basic Hallo wereld-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="1587c-114">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="1587c-115">Hallo-toepassing wordt gehost in Azure een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1587c-115">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="1587c-116">Hallo volgende schermafbeelding ziet u de toepassing hello voltooid:</span><span class="sxs-lookup"><span data-stu-id="1587c-116">hello following screenshot shows hello completed application:</span></span>

![Een browservenster Hallo Hallo wereldpagina wordt weergegeven in Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="1587c-118">Maken en een virtuele machine van Azure toohost Django instellen</span><span class="sxs-lookup"><span data-stu-id="1587c-118">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="1587c-119">een virtuele machine van Azure met Hallo distributie van Windows Server 2012 R2 Datacenter, toocreate Zie [maken van een virtuele machine met Windows in hello Azure-portal](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="1587c-119">toocreate an Azure virtual machine with hello Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="1587c-120">Azure toodirect poort 80 verkeer van Hallo web tooport 80 op Hallo virtuele machine instellen:</span><span class="sxs-lookup"><span data-stu-id="1587c-120">Set Azure toodirect port 80 traffic from hello web tooport 80 on hello virtual machine:</span></span>
   
   1. <span data-ttu-id="1587c-121">In hello Azure-portal, gaat u toohello dashboard en selecteer de zojuist gemaakte virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1587c-121">In hello Azure portal, go toohello dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="1587c-122">Klik op **Eindpunten** en vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1587c-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Een eindpunt toevoegen](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="1587c-124">Op Hallo **eindpunt toevoegen** pagina voor **naam**, voer **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="1587c-124">On hello **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="1587c-125">Hallo openbare en persoonlijke TCP-poorten te ingesteld**80**.</span><span class="sxs-lookup"><span data-stu-id="1587c-125">Set hello public and private TCP ports too**80**.</span></span>

     ![Naam en openbare en particuliere poort instellen](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="1587c-127">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1587c-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="1587c-128">Selecteer uw virtuele machine in Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="1587c-128">In hello dashboard, select your VM.</span></span> <span data-ttu-id="1587c-129">toouse Remote Desktop Protocol (RDP) tooremotely aanmelden toohello nieuw gemaakte virtuele machine van Azure, klikt u op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="1587c-129">toouse Remote Desktop Protocol (RDP) tooremotely sign in toohello newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="1587c-130">Hallo instructies wordt ervan uitgegaan dat u in de toohello virtuele machine correct ondertekend.</span><span class="sxs-lookup"><span data-stu-id="1587c-130">hello following instructions assume that you signed in toohello virtual machine correctly.</span></span> <span data-ttu-id="1587c-131">Ze ook wordt ervan uitgegaan dat dat u opdrachten in Hallo virtuele machine en niet op uw lokale computer uitvoert.</span><span class="sxs-lookup"><span data-stu-id="1587c-131">They also assume that you are issuing commands in hello virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="1587c-132"><a id="setup"></a>Python en Django WFastCGI installeren</span><span class="sxs-lookup"><span data-stu-id="1587c-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="1587c-133">toodownload met behulp van Internet Explorer, moet u Internet Explorer tooconfigure wellicht **verbeterde beveiliging** instellingen.</span><span class="sxs-lookup"><span data-stu-id="1587c-133">toodownload by using Internet Explorer, you might have tooconfigure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="1587c-134">toodo, klikt u op **Start** > **Systeembeheer** > **Serverbeheer** > **lokale Server**.</span><span class="sxs-lookup"><span data-stu-id="1587c-134">toodo this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="1587c-135">Klik op **verbeterde beveiliging van Internet Explorer**, en selecteer vervolgens **uit**.</span><span class="sxs-lookup"><span data-stu-id="1587c-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="1587c-136">Installeren van de meest recente versies Hallo van Python 2.7 of 3.4 van Python [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="1587c-136">Install hello latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="1587c-137">Hello-pakketten wfastcgi en django met behulp van pip installeren.</span><span class="sxs-lookup"><span data-stu-id="1587c-137">Install hello wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="1587c-138">Gebruik voor Python 2.7 Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="1587c-138">For Python 2.7, use hello following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="1587c-139">Gebruik voor Python 3.4 Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="1587c-139">For Python 3.4, use hello following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="1587c-140">IIS met FastCGI installeren</span><span class="sxs-lookup"><span data-stu-id="1587c-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="1587c-141">Internet Information Services (IIS) installeren met de ondersteuning van FastCGI.</span><span class="sxs-lookup"><span data-stu-id="1587c-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="1587c-142">Dit kan enkele minuten tooexecute duren.</span><span class="sxs-lookup"><span data-stu-id="1587c-142">This might take several minutes tooexecute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="1587c-143">Maak een nieuwe Django-toepassing</span><span class="sxs-lookup"><span data-stu-id="1587c-143">Create a new Django application</span></span>
1. <span data-ttu-id="1587c-144">Voer in C:\inetpub\wwwroot, een nieuw project Django toocreate Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="1587c-144">In C:\inetpub\wwwroot, toocreate a new Django project, enter hello following command:</span></span>
   
   <span data-ttu-id="1587c-145">Gebruik voor Python 2.7 Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="1587c-145">For Python 2.7, use hello following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="1587c-146">Gebruik voor Python 3.4 Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="1587c-146">For Python 3.4, use hello following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![Hallo resultaat van de opdracht Hallo New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="1587c-148">Hallo `django-admin` opdracht genereert een basisstructuur voor Django-gebaseerde websites:</span><span class="sxs-lookup"><span data-stu-id="1587c-148">hello `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="1587c-149">`helloworld\manage.py`helpt u te hosten en stoppen met het hosten van uw website op basis van een Django.</span><span class="sxs-lookup"><span data-stu-id="1587c-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="1587c-150">`helloworld\helloworld\settings.py`Django-instellingen voor de toepassing is.</span><span class="sxs-lookup"><span data-stu-id="1587c-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="1587c-151">`helloworld\helloworld\urls.py`heeft Hallo toewijzing code tussen elke URL en de weergave.</span><span class="sxs-lookup"><span data-stu-id="1587c-151">`helloworld\helloworld\urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="1587c-152">In Hallo C:\inetpub\wwwroot\helloworld\helloworld directory, maakt u een nieuw bestand met de naam views.py.</span><span class="sxs-lookup"><span data-stu-id="1587c-152">In hello C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="1587c-153">Dit bestand heeft Hallo weergeven dat Hallo "Hallo wereld" pagina weergeeft.</span><span class="sxs-lookup"><span data-stu-id="1587c-153">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="1587c-154">Voer in de code-editor Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="1587c-154">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="1587c-155">Hallo-inhoud van Hallo urls.py bestand vervangen door Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="1587c-155">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="1587c-156">Instellen van IIS</span><span class="sxs-lookup"><span data-stu-id="1587c-156">Set up IIS</span></span>
1. <span data-ttu-id="1587c-157">In bestand van de globale applicationhost.config hello, Hallo handlers sectie te ontgrendelen.</span><span class="sxs-lookup"><span data-stu-id="1587c-157">In hello global applicationhost.config file, unlock hello handlers section.</span></span>  <span data-ttu-id="1587c-158">Hierdoor is het web.config-bestand toouse Hallo Python-handler.</span><span class="sxs-lookup"><span data-stu-id="1587c-158">This allows your web.config file toouse hello Python handler.</span></span> <span data-ttu-id="1587c-159">Deze opdracht toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1587c-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="1587c-160">WFastCGI activeren.</span><span class="sxs-lookup"><span data-stu-id="1587c-160">Activate WFastCGI.</span></span> <span data-ttu-id="1587c-161">Hiermee wordt een toepassing toohello globale applicationhost.config bestand, dat tooyour Python-interpreter executable en Hallo wfastcgi.py script verwijst toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1587c-161">This adds an application toohello global applicationhost.config file, which refers tooyour Python interpreter executable and hello wfastcgi.py script.</span></span>
   
    <span data-ttu-id="1587c-162">In Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="1587c-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="1587c-163">In Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="1587c-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="1587c-164">In C:\inetpub\wwwroot\helloworld, maakt u een web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="1587c-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="1587c-165">waarde van Hallo Hallo `scriptProcessor` kenmerk moet overeenkomen met de Hallo-uitvoer van de voorgaande stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="1587c-165">hello value of hello `scriptProcessor` attribute should match hello output from hello preceding step.</span></span> <span data-ttu-id="1587c-166">Zie voor meer informatie over het instellen van Hallo wfastcgi [pypi wfastcgi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="1587c-166">For more information about hello wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="1587c-167">In Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="1587c-167">In  Python 2.7:</span></span>
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python27\python.exe|C:\Python27\Lib\site-packages\wfastcgi.pyc" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
   
   <span data-ttu-id="1587c-168">In Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="1587c-168">In  Python 3.4:</span></span>
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python34\python.exe|C:\Python34\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
4. <span data-ttu-id="1587c-169">Hallo-locatie van Hallo IIS standaard website toopoint toohello Django projectmap bijwerken:</span><span class="sxs-lookup"><span data-stu-id="1587c-169">Update hello location of hello IIS default website toopoint toohello Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="1587c-170">Hallo webpagina in uw browser worden geladen.</span><span class="sxs-lookup"><span data-stu-id="1587c-170">Load hello webpage in your browser.</span></span>

![Een browservenster weergegeven Hallo Hallo wereld-pagina op Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="1587c-172">De virtuele machine van Azure afsluiten</span><span class="sxs-lookup"><span data-stu-id="1587c-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="1587c-173">Wanneer u met deze zelfstudie bent klaar, wordt aangeraden u afgesloten of hello Azure VM die u hebt gemaakt voor de zelfstudie Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1587c-173">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="1587c-174">Hiermee wordt vrijgemaakt bronnen voor andere zelfstudies en kunt u voorkomen dat Azure gebruikskosten aangaan.</span><span class="sxs-lookup"><span data-stu-id="1587c-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi

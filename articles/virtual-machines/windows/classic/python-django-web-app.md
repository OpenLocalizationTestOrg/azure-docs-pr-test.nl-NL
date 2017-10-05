---
title: Django-web-app op een Windows Server Azure VM | Microsoft Docs
description: Informatie over het hosten van een website op basis van Django in Azure met behulp van een VM van Windows Server 2012 R2 Datacenter met het klassieke implementatiemodel.
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
ms.openlocfilehash: 283a296fb39863c2801be1093cc4f56904786abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="49f44-103">Django Hallo wereld-web-app op een virtuele machine van Windows Server</span><span class="sxs-lookup"><span data-stu-id="49f44-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="49f44-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en het klassieke implementatiemodel](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="49f44-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and the classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="49f44-105">Dit artikel wordt beschreven voor het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="49f44-105">This article describes the classic deployment model.</span></span> <span data-ttu-id="49f44-106">U wordt aangeraden de meeste nieuwe implementaties het Resource Manager-model gebruiken.</span><span class="sxs-lookup"><span data-stu-id="49f44-106">We recommend that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="49f44-107">Deze zelfstudie laat zien hoe u voor het hosten van een website op basis van Django in Windows Server in Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="49f44-107">This tutorial shows you how to host a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="49f44-108">In de zelfstudie gaan we ervan uit geen ervaring met Azure.</span><span class="sxs-lookup"><span data-stu-id="49f44-108">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="49f44-109">Wanneer u de zelfstudie hebt voltooid, hebt u een toepassing op basis van de Django up en wordt uitgevoerd in de cloud.</span><span class="sxs-lookup"><span data-stu-id="49f44-109">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="49f44-110">Leer hoe u het volgende doet:</span><span class="sxs-lookup"><span data-stu-id="49f44-110">Learn how to:</span></span>

* <span data-ttu-id="49f44-111">Een virtuele machine van Azure naar host Django instellen.</span><span class="sxs-lookup"><span data-stu-id="49f44-111">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="49f44-112">Hoewel deze zelfstudie wordt uitgelegd hoe u dit doen voor **Windows Server**, kunt u dezelfde doen voor een Linux-VM wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="49f44-112">Although this tutorial explains how to do this for **Windows Server**, you can do the same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="49f44-113">Maak een nieuwe Django-toepassing in Windows.</span><span class="sxs-lookup"><span data-stu-id="49f44-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="49f44-114">De zelfstudie laat zien hoe een basic Hallo wereld-webtoepassing bouwen.</span><span class="sxs-lookup"><span data-stu-id="49f44-114">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="49f44-115">De toepassing wordt gehost in Azure een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49f44-115">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="49f44-116">De volgende schermafbeelding ziet de voltooide toepassing:</span><span class="sxs-lookup"><span data-stu-id="49f44-116">The following screenshot shows the completed application:</span></span>

![Een browservenster weergegeven Hallo wereld-pagina in Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="49f44-118">Maken en een virtuele machine van Azure naar host Django instellen</span><span class="sxs-lookup"><span data-stu-id="49f44-118">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="49f44-119">Zie voor informatie over het maken van een virtuele machine van Azure met de distributie van Windows Server 2012 R2 Datacenter [maken van een virtuele machine waarop Windows wordt uitgevoerd in de Azure portal](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="49f44-119">To create an Azure virtual machine with the Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="49f44-120">Instellen van Azure naar poort 80 verkeer via het web naar poort 80 op de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="49f44-120">Set Azure to direct port 80 traffic from the web to port 80 on the virtual machine:</span></span>
   
   1. <span data-ttu-id="49f44-121">In de Azure-portal, gaat u naar het dashboard en selecteer de zojuist gemaakte virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49f44-121">In the Azure portal, go to the dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="49f44-122">Klik op **Eindpunten** en vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="49f44-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Een eindpunt toevoegen](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="49f44-124">Op de **eindpunt toevoegen** pagina voor **naam**, voer **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="49f44-124">On the **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="49f44-125">De openbare en persoonlijke TCP-poorten instellen op **80**.</span><span class="sxs-lookup"><span data-stu-id="49f44-125">Set the public and private TCP ports to **80**.</span></span>

     ![Naam en openbare en particuliere poort instellen](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="49f44-127">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="49f44-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="49f44-128">Selecteer in het dashboard van de VM.</span><span class="sxs-lookup"><span data-stu-id="49f44-128">In the dashboard, select your VM.</span></span> <span data-ttu-id="49f44-129">Met Remote Desktop Protocol (RDP) extern aanmelden bij de zojuist gemaakte virtuele machine van Azure, klikt u op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="49f44-129">To use Remote Desktop Protocol (RDP) to remotely sign in to the newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="49f44-130">De volgende instructies wordt ervan uitgegaan dat u de virtuele machine correct ondertekend.</span><span class="sxs-lookup"><span data-stu-id="49f44-130">The following instructions assume that you signed in to the virtual machine correctly.</span></span> <span data-ttu-id="49f44-131">Ze ook wordt ervan uitgegaan dat dat u opdrachten in de virtuele machine en niet op uw lokale computer uitvoert.</span><span class="sxs-lookup"><span data-stu-id="49f44-131">They also assume that you are issuing commands in the virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="49f44-132"><a id="setup"></a>Python en Django WFastCGI installeren</span><span class="sxs-lookup"><span data-stu-id="49f44-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="49f44-133">Als u wilt downloaden met behulp van Internet Explorer, mogelijk moet Internet Explorer configureren **verbeterde beveiliging** instellingen.</span><span class="sxs-lookup"><span data-stu-id="49f44-133">To download by using Internet Explorer, you might have to configure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="49f44-134">Om dit te doen, klikt u op **Start** > **Systeembeheer** > **Serverbeheer** > **lokale Server**.</span><span class="sxs-lookup"><span data-stu-id="49f44-134">To do this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="49f44-135">Klik op **verbeterde beveiliging van Internet Explorer**, en selecteer vervolgens **uit**.</span><span class="sxs-lookup"><span data-stu-id="49f44-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="49f44-136">Installeer de nieuwste versie van Python 2.7 of 3.4 van Python [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="49f44-136">Install the latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="49f44-137">De met behulp van pip wfastcgi en django-pakketten installeren.</span><span class="sxs-lookup"><span data-stu-id="49f44-137">Install the wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="49f44-138">Gebruik de volgende opdracht voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="49f44-138">For Python 2.7, use the following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="49f44-139">Gebruik de volgende opdracht voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="49f44-139">For Python 3.4, use the following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="49f44-140">IIS met FastCGI installeren</span><span class="sxs-lookup"><span data-stu-id="49f44-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="49f44-141">Internet Information Services (IIS) installeren met de ondersteuning van FastCGI.</span><span class="sxs-lookup"><span data-stu-id="49f44-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="49f44-142">Dit kan enige tijd duren om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="49f44-142">This might take several minutes to execute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="49f44-143">Maak een nieuwe Django-toepassing</span><span class="sxs-lookup"><span data-stu-id="49f44-143">Create a new Django application</span></span>
1. <span data-ttu-id="49f44-144">In C:\inetpub\wwwroot, om een nieuwe Django-project maakt, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="49f44-144">In C:\inetpub\wwwroot, to create a new Django project, enter the following command:</span></span>
   
   <span data-ttu-id="49f44-145">Gebruik de volgende opdracht voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="49f44-145">For Python 2.7, use the following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="49f44-146">Gebruik de volgende opdracht voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="49f44-146">For Python 3.4, use the following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![Het resultaat van de opdracht New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="49f44-148">De `django-admin` opdracht genereert een basisstructuur voor Django-gebaseerde websites:</span><span class="sxs-lookup"><span data-stu-id="49f44-148">The `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="49f44-149">`helloworld\manage.py`helpt u te hosten en stoppen met het hosten van uw website op basis van een Django.</span><span class="sxs-lookup"><span data-stu-id="49f44-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="49f44-150">`helloworld\helloworld\settings.py`Django-instellingen voor de toepassing is.</span><span class="sxs-lookup"><span data-stu-id="49f44-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="49f44-151">`helloworld\helloworld\urls.py`heeft de code van de toewijzing tussen elke URL en de weergave.</span><span class="sxs-lookup"><span data-stu-id="49f44-151">`helloworld\helloworld\urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="49f44-152">Maak een nieuw bestand met de naam views.py in de map C:\inetpub\wwwroot\helloworld\helloworld.</span><span class="sxs-lookup"><span data-stu-id="49f44-152">In the C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="49f44-153">Dit bestand heeft de weergave die de pagina "Hallo wereld geeft".</span><span class="sxs-lookup"><span data-stu-id="49f44-153">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="49f44-154">Voer de volgende opdrachten in de code-editor:</span><span class="sxs-lookup"><span data-stu-id="49f44-154">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="49f44-155">De inhoud van het bestand urls.py vervangen door de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="49f44-155">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="49f44-156">Instellen van IIS</span><span class="sxs-lookup"><span data-stu-id="49f44-156">Set up IIS</span></span>
1. <span data-ttu-id="49f44-157">In het bestand applicationhost.config globale ontgrendelen de sectie-handlers.</span><span class="sxs-lookup"><span data-stu-id="49f44-157">In the global applicationhost.config file, unlock the handlers section.</span></span>  <span data-ttu-id="49f44-158">Hierdoor kan het bestand web.config, het Python-handler moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="49f44-158">This allows your web.config file to use the Python handler.</span></span> <span data-ttu-id="49f44-159">Deze opdracht toevoegen:</span><span class="sxs-lookup"><span data-stu-id="49f44-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="49f44-160">WFastCGI activeren.</span><span class="sxs-lookup"><span data-stu-id="49f44-160">Activate WFastCGI.</span></span> <span data-ttu-id="49f44-161">Hiermee wordt een toepassing op het bestand applicationhost.config globale, dat naar uw uitvoerbare Python-interpreter en het script wfastcgi.py verwijst toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="49f44-161">This adds an application to the global applicationhost.config file, which refers to your Python interpreter executable and the wfastcgi.py script.</span></span>
   
    <span data-ttu-id="49f44-162">In Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="49f44-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="49f44-163">In Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="49f44-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="49f44-164">In C:\inetpub\wwwroot\helloworld, maakt u een web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="49f44-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="49f44-165">De waarde van de `scriptProcessor` kenmerk moet overeenkomen met de uitvoer van de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="49f44-165">The value of the `scriptProcessor` attribute should match the output from the preceding step.</span></span> <span data-ttu-id="49f44-166">Zie voor meer informatie over de instelling wfastcgi [pypi wfastcgi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="49f44-166">For more information about the wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="49f44-167">In Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="49f44-167">In  Python 2.7:</span></span>
   
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
   
   <span data-ttu-id="49f44-168">In Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="49f44-168">In  Python 3.4:</span></span>
   
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
4. <span data-ttu-id="49f44-169">De locatie van de standaardwebsite van IIS om te verwijzen naar de projectmap Django bijwerken:</span><span class="sxs-lookup"><span data-stu-id="49f44-169">Update the location of the IIS default website to point to the Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="49f44-170">Laad de webpagina die in uw browser.</span><span class="sxs-lookup"><span data-stu-id="49f44-170">Load the webpage in your browser.</span></span>

![Een browservenster weergegeven Hallo wereld-pagina op Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="49f44-172">De virtuele machine van Azure afsluiten</span><span class="sxs-lookup"><span data-stu-id="49f44-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="49f44-173">Wanneer u met deze zelfstudie bent klaar, raden we aan u afgesloten of verwijder de Azure virtuele machine die u hebt gemaakt voor de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="49f44-173">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="49f44-174">Hiermee wordt vrijgemaakt bronnen voor andere zelfstudies en kunt u voorkomen dat Azure gebruikskosten aangaan.</span><span class="sxs-lookup"><span data-stu-id="49f44-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi

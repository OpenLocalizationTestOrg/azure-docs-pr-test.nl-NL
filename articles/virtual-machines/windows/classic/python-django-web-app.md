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
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a>Django Hallo wereld-web-app op een virtuele machine van Windows Server

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en Hallo klassieke implementatiemodel](../../../resource-manager-deployment-model.md). Dit artikel wordt beschreven Hallo klassieke implementatiemodel. U wordt aangeraden de meeste nieuwe implementaties Hallo Resource Manager-model gebruiken.

Deze zelfstudie leert u hoe toohost een website op basis van Django in Windows Server in Azure Virtual Machines. In de zelfstudie Hallo we ervan uitgaan dat geen ervaring met Azure. Wanneer u Hallo-zelfstudie hebt voltooid, hebt u een Django-toepassing up en wordt uitgevoerd in de cloud Hallo.

Leer hoe u het volgende doet:

* Instellen van een virtuele machine van Azure toohost Django. Hoewel deze zelfstudie wordt uitgelegd hoe toodo dit voor **Windows Server**, kunt u doen Hallo dezelfde voor een Linux-VM wordt gehost in Azure.
* Maak een nieuwe Django-toepassing in Windows.

Hallo-zelfstudie laat zien hoe toobuild een basic Hallo wereld-webtoepassing. Hallo-toepassing wordt gehost in Azure een virtuele machine.

Hallo volgende schermafbeelding ziet u de toepassing hello voltooid:

![Een browservenster Hallo Hallo wereldpagina wordt weergegeven in Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Maken en een virtuele machine van Azure toohost Django instellen

1. een virtuele machine van Azure met Hallo distributie van Windows Server 2012 R2 Datacenter, toocreate Zie [maken van een virtuele machine met Windows in hello Azure-portal](tutorial.md).
2. Azure toodirect poort 80 verkeer van Hallo web tooport 80 op Hallo virtuele machine instellen:
   
   1. In hello Azure-portal, gaat u toohello dashboard en selecteer de zojuist gemaakte virtuele machine.
   2. Klik op **Eindpunten** en vervolgens op **Toevoegen**.

     ![Een eindpunt toevoegen](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. Op Hallo **eindpunt toevoegen** pagina voor **naam**, voer **HTTP**. Hallo openbare en persoonlijke TCP-poorten te ingesteld**80**.

     ![Naam en openbare en particuliere poort instellen](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. Klik op **OK**.
     
3. Selecteer uw virtuele machine in Hallo-dashboard. toouse Remote Desktop Protocol (RDP) tooremotely aanmelden toohello nieuw gemaakte virtuele machine van Azure, klikt u op **Connect**.  

> [!IMPORTANT] 
> Hallo instructies wordt ervan uitgegaan dat u in de toohello virtuele machine correct ondertekend. Ze ook wordt ervan uitgegaan dat dat u opdrachten in Hallo virtuele machine en niet op uw lokale computer uitvoert.

## <a id="setup"></a>Python en Django WFastCGI installeren
> [!NOTE]
> toodownload met behulp van Internet Explorer, moet u Internet Explorer tooconfigure wellicht **verbeterde beveiliging** instellingen. toodo, klikt u op **Start** > **Systeembeheer** > **Serverbeheer** > **lokale Server**. Klik op **verbeterde beveiliging van Internet Explorer**, en selecteer vervolgens **uit**.

1. Installeren van de meest recente versies Hallo van Python 2.7 of 3.4 van Python [python.org][python.org].
2. Hello-pakketten wfastcgi en django met behulp van pip installeren.
   
    Gebruik voor Python 2.7 Hallo volgende opdracht:
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    Gebruik voor Python 3.4 Hallo volgende opdracht:
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a>IIS met FastCGI installeren
* Internet Information Services (IIS) installeren met de ondersteuning van FastCGI. Dit kan enkele minuten tooexecute duren.
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a>Maak een nieuwe Django-toepassing
1. Voer in C:\inetpub\wwwroot, een nieuw project Django toocreate Hallo volgende opdracht:
   
   Gebruik voor Python 2.7 Hallo volgende opdracht:
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   Gebruik voor Python 3.4 Hallo volgende opdracht:
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![Hallo resultaat van de opdracht Hallo New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. Hallo `django-admin` opdracht genereert een basisstructuur voor Django-gebaseerde websites:
   
   * `helloworld\manage.py`helpt u te hosten en stoppen met het hosten van uw website op basis van een Django.
   * `helloworld\helloworld\settings.py`Django-instellingen voor de toepassing is.
   * `helloworld\helloworld\urls.py`heeft Hallo toewijzing code tussen elke URL en de weergave.
3. In Hallo C:\inetpub\wwwroot\helloworld\helloworld directory, maakt u een nieuw bestand met de naam views.py. Dit bestand heeft Hallo weergeven dat Hallo "Hallo wereld" pagina weergeeft. Voer in de code-editor Hallo volgende opdrachten:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Hallo-inhoud van Hallo urls.py bestand vervangen door Hallo volgende opdrachten:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a>Instellen van IIS
1. In bestand van de globale applicationhost.config hello, Hallo handlers sectie te ontgrendelen.  Hierdoor is het web.config-bestand toouse Hallo Python-handler. Deze opdracht toevoegen:
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. WFastCGI activeren. Hiermee wordt een toepassing toohello globale applicationhost.config bestand, dat tooyour Python-interpreter executable en Hallo wfastcgi.py script verwijst toegevoegd.
   
    In Python 2.7:
   
        C:\python27\scripts\wfastcgi-enable
   
    In Python 3.4:
   
        C:\python34\scripts\wfastcgi-enable
3. In C:\inetpub\wwwroot\helloworld, maakt u een web.config-bestand. waarde van Hallo Hallo `scriptProcessor` kenmerk moet overeenkomen met de Hallo-uitvoer van de voorgaande stap Hallo. Zie voor meer informatie over het instellen van Hallo wfastcgi [pypi wfastcgi][wfastcgi].
   
   In Python 2.7:
   
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
   
   In Python 3.4:
   
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
4. Hallo-locatie van Hallo IIS standaard website toopoint toohello Django projectmap bijwerken:
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. Hallo webpagina in uw browser worden geladen.

![Een browservenster weergegeven Hallo Hallo wereld-pagina op Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a>De virtuele machine van Azure afsluiten
Wanneer u met deze zelfstudie bent klaar, wordt aangeraden u afgesloten of hello Azure VM die u hebt gemaakt voor de zelfstudie Hallo verwijderen. Hiermee wordt vrijgemaakt bronnen voor andere zelfstudies en kunt u voorkomen dat Azure gebruikskosten aangaan.

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi

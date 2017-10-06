---
title: aaaConfiguring Python met Azure App Service Web Apps
description: Deze zelfstudie wordt beschreven opties voor het ontwerpen en configureren van een eenvoudige webserver Gateway Interface (WSGI) compatibele Python-toepassing in Azure App Service Web Apps.
services: app-service
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 00d49fb01491e9adb4b6fededfb95669a8dbd485
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a>Python configureren met Azure App Service WebApps
Deze zelfstudie wordt beschreven opties voor het ontwerpen en configureren van een eenvoudige Web Server Gateway Interface (WSGI) compatibele Python-toepassing op [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Aanvullende functies van Git-implementatie, zoals virtuele omgeving en de installatie van het pakket met requirements.txt beschrijft.

## <a name="bottle-django-or-flask"></a>Bottle, Django of Flask?
Hello Azure Marketplace bevat sjablonen voor Hallo Bottle, Django en Flask frameworks. Als u uw eerste web-app in Azure App Service ontwikkelt, of u niet bekend met Git bent, raden wij aan dat u deze zelfstudies, waaronder Stapsgewijze instructies volgt voor het bouwen van een werkende toepassing uit Hallo galerie met Git-implementatie in Windows of Mac:

* [Web-apps maken met Bottle](web-sites-python-create-deploy-bottle-app.md)
* [Web-apps maken met Django](web-sites-python-create-deploy-django-app.md)
* [Web-apps maken met Flask](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a>Web-Apps maken op Azure-Portal
Deze zelfstudie wordt ervan uitgegaan van een bestaande Azure-abonnement en toegang toohello Azure-Portal.

Als u een bestaande web-app niet hebt, kunt u één van Hallo [Azure Portal](https://portal.azure.com).  Klik op de nieuwe knop Hallo in Hallo linksboven en klik vervolgens op **Web en mobiel** > **Web-app**.

## <a name="git-publishing"></a>GIT-publicatie
Configureer Git-publicatie voor uw nieuwe web-app met behulp Hallo-instructies in [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md). Deze zelfstudie wordt gebruikgemaakt van Git toocreate, beheren en publiceren van onze Python web app tooAzure App Service.

Zodra de Git-publicatie is ingesteld, wordt een Git-opslagplaats gemaakt en gekoppeld aan uw web-app. Hallo-opslagplaats URL kan wordt weergegeven en voortaan gebruikte toopush gegevens uit Hallo lokale ontwikkeling omgeving toohello cloud. toopublish toepassingen via Git, Controleer of een Git-client is geïnstalleerd en gebruik Hallo instructies toopush uw web-app inhoud tooAzure App Service.

## <a name="application-overview"></a>Toepassingsoverzicht
In de volgende secties Hallo worden Hallo volgende bestanden gemaakt. Ze moeten worden geplaatst in de hoofdmap Hallo van Hallo Git-opslagplaats.

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a>WSGI-Handler
WSGI is een Python-standaard beschreven door [PEP 3333](http://www.python.org/dev/peps/pep-3333/) definiëren van een interface tussen de webserver Hallo en Python. Dit biedt een gestandaardiseerde interface voor het schrijven van verschillende webtoepassingen en frameworks met behulp van Python. Populaire frameworks voor Python-web gebruik vandaag WSGI. Azure App Service Web Apps biedt die u ondersteuning voor dergelijke frameworks; Bovendien kunnen advanced-gebruikers ook schrijven hun eigen zolang Hallo aangepaste handler Hallo WSGI specificatie richtlijnen volgt.

Hier volgt een voorbeeld van een `app.py` waarmee wordt gedefinieerd met een aangepaste handler:

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

U kunt deze toepassing lokaal met uitvoeren `python app.py`, bladert u te`http://localhost:5555` in uw webbrowser.

## <a name="virtual-environment"></a>Virtuele omgeving
Hoewel bovenstaande Hallo voorbeeld-app niet zijn voor alle externe pakketten vereist, is het waarschijnlijk dat uw toepassing enkele wordt vereist.

toohelp beheer van externe pakketafhankelijkheden, Azure Git-implementatie ondersteunt het Hallo maken van virtuele omgevingen.

Als Azure een requirements.txt in de hoofdmap Hallo van Hallo-opslagplaats detecteert, wordt automatisch een virtuele omgeving met de naam gemaakt `env`. Dit gebeurt alleen bij de eerste implementatie Hallo of tijdens een implementatie na Hallo geselecteerde Python-runtime is gewijzigd.

U wilt waarschijnlijk toocreate een virtuele omgeving lokaal voor ontwikkeling, maar niet opnemen in de Git-opslagplaats.

## <a name="package-management"></a>Pakketbeheer
Pakketten die worden vermeld in requirements.txt worden automatisch geïnstalleerd in de virtuele omgeving Hallo via pip. Dit gebeurt op elke implementatie, maar pip slaat de installatie over als u een pakket is al geïnstalleerd.

Voorbeeld `requirements.txt`:

    azure==0.8.4


## <a name="python-version"></a>Python-versie
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

Voorbeeld `runtime.txt`:

    python-2.7


## <a name="webconfig"></a>Web.config
U moet een web.config-bestand toospecify toocreate hoe Hallo-server aanvragen moet verwerken.

Houd er rekening mee dat als er een web.x.y.config-bestand in de opslagplaats, waar x.y overeenkomt met Hallo Python-runtime geselecteerde en Azure automatisch de juiste bestand Hallo als web.config kopieert.

Hallo volgende web.config voorbeelden zijn afhankelijk van een virtuele omgeving proxyscript die wordt beschreven in de volgende sectie Hallo.  Ze werken met Hallo WSGI handler die wordt gebruikt in Hallo voorbeeld `app.py` hierboven.

Voorbeeld `web.config` voor Python 2.7:

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


Voorbeeld `web.config` voor Python 3.4:

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


Statische bestanden wordt verwerkt door de webserver Hallo rechtstreeks, zonder tussenkomst van Python-code, voor betere prestaties.

Hallo-locatie van statische bestanden op schijf Hallo moet overeenkomen met Hallo locatie in Hallo-URL in Hallo bovenstaande voorbeelden. Dit betekent dat een aanvraag voor `http://pythonapp.azurewebsites.net/static/site.css` fungeert Hallo-bestand op de schijf op `\static\site.css`.

`WSGI_ALT_VIRTUALENV_HANDLER`is waar u Hallo WSGI handler opgeven. In Hallo bovenstaande voorbeelden, hieraan `app.wsgi_app` omdat Hallo-handler een functie met de naam is `wsgi_app` in `app.py` in Hallo-hoofdmap.

`PYTHONPATH`kan worden aangepast, maar als u alle afhankelijkheden in de virtuele omgeving Hallo installeert door te geven ze in requirements.txt, toochange niet nodig deze.

## <a name="virtual-environment-proxy"></a>Virtuele omgeving Proxy
Hallo script volgen gebruikte tooretrieve hello WSGI handler, Hallo virtuele omgeving en logboek fouten activeren. Het is ontworpen toobe algemene en die wordt gebruikt zonder wijzigingen.

Inhoud van `ptvs_virtualenv_proxy.py`:

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject tooterms and conditions of hello Apache License, Version 2.0. A 
     # copy of hello license can be found in hello License.html file at hello root of this distribution. If 
     # you cannot locate hello Apache License, Version 2.0, please send an email too
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing toobe bound 
     # by hello terms of hello Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors tooa log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a>Git-implementatie aanpassen
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a>Probleemoplossing - Installatie van pakketten
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Probleemoplossing - Virtuele omgeving
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, Hallo [Python Developer Center](/develop/python/).

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)


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
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>Django Hallo wereld-web-app op een Linux-VM
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

Deze zelfstudie leert u hoe toohost een website op basis van Django in Linux in Azure Virtual Machines. In de zelfstudie Hallo we ervan uitgaan dat geen ervaring met Azure. Wanneer u Hallo-zelfstudie hebt voltooid, hebt u een Django-toepassing up en wordt uitgevoerd in de cloud Hallo.

Leer hoe u het volgende doet:

* Instellen van een virtuele machine van Azure toohost Django. Hoewel deze zelfstudie wordt uitgelegd hoe toodo dit voor **Linux**, kunt u doen hello dezelfde voor een Windows Server-VM gehost in Azure. 
* Een nieuwe Django-toepassing maken in Linux.

Hallo-zelfstudie laat zien hoe toobuild een basic Hallo wereld-webtoepassing. Hallo-toepassing wordt gehost in Azure een virtuele machine.

Hallo volgende schermafbeelding ziet u de toepassing hello voltooid:

![Hallo Hallo wereld-pagina in een browservenster wordt weergegeven in Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Maken en een virtuele machine van Azure toohost Django instellen

1. toocreate een virtuele machine van Azure met Hallo Ubuntu Server 14.04 TNS distributie, Zie [virtuele Linux-machine maken in Azure-portal Hallo](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). U kunt ook wachtwoordverificatie in plaats van een openbare SSH-sleutel.
2. tooedit hello network security groep tooallow binnenkomende HTTP-verkeer tooport 80, Zie [netwerkbeveiligingsgroepen maken in Azure-portal Hallo](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).
3. (Optioneel) Uw nieuwe virtuele machine geen standaard een volledig gekwalificeerde domeinnaam (FQDN).  een virtuele machine met een FQDN toocreate Zie [maken van een FQDN-naam in hello Azure-portal voor een virtuele machine van Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Deze stap is niet vereist voor het voltooien van deze zelfstudie.

## <a id="setup"></a>Hello ontwikkelomgeving instellen
> [!NOTE]
> Als u Python tooinstall moet of toouse Hallo clientbibliotheken wilt, raadpleegt u Hallo [Python installatiehandleiding](../../python-how-to-install.md).

Hallo Ubuntu Linux VM heeft Python 2.7 vooraf geïnstalleerd, maar deze wordt niet geleverd met Apache of Django. Volgende stappen tooconnect tooyour VM Hallo voltooien en Apache en Django te installeren:

1. Open een nieuw venster van de Terminal.
2. tooconnect toohello Azure virtuele machine, Voer Hallo na de opdracht. Als u een FQDN-naam hebt gemaakt, kunt u verbinding maken met behulp van het openbare IP-adres hello, die wordt weergegeven in de Hallo virtuele machine samenvatting in hello Azure-portal.
   
       $ ssh yourusername@yourVmUrl
3. tooinstall Django, Voer Hallo volgende opdrachten:
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. tooinstall Apache met rest-wsgi Voer Hallo volgende opdracht:
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>Een nieuwe Django-app maken
1. toouse SSH tooaccess uw VM, open Hallo terminalvenster u in de voorgaande sectie Hallo gebruikt.
2. toocreate een nieuwe Django-project, geef Hallo volgende opdrachten:
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   Hallo `django-admin.py` script genereert een basisstructuur voor Django-gebaseerde websites:
   
   * `helloworld/manage.py`helpt u te hosten en stoppen met het hosten van uw website op basis van een Django.
   * `helloworld/helloworld/settings.py`Django-instellingen voor de toepassing is.
   * `helloworld/helloworld/urls.py`heeft Hallo toewijzing code tussen elke URL en de weergave.
3. In Hallo /var/www/helloworld/helloworld directory, maakt u een nieuw bestand met de naam views.py. Dit bestand heeft Hallo weergeven dat Hallo "Hallo wereld" pagina weergeeft. Voer in de code-editor Hallo volgende opdrachten:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Hallo-inhoud van Hallo urls.py bestand vervangen door Hallo volgende opdrachten:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>Apache instellen
1. Maak een Apache virtuele host-configuratiebestand in Hallo /etc/apache2/sites-available/helloworld.conf map. Hallo inhoud toohello volgende waarden ingesteld. Vervang *yourVmName* met Hallo werkelijke naam van de door u gebruikte computer hello (bijvoorbeeld *pyubuntu*).
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. tooactivate hello site gebruik Hallo volgende opdracht:
   
       $ sudo a2ensite helloworld
3. toorestart Apache Hallo volgende opdracht gebruiken:
   
       $ sudo service apache2 reload
4. Hallo webpagina in uw browser worden geladen:
   
   ![Een browservenster Hallo Hallo wereldpagina wordt weergegeven in Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>De virtuele machine van Azure afsluiten
Wanneer u met deze zelfstudie bent klaar, wordt aangeraden u afgesloten of hello Azure VM die u hebt gemaakt voor de zelfstudie Hallo verwijderen. Hiermee wordt vrijgemaakt bronnen voor andere zelfstudies en kunt u voorkomen dat Azure gebruikskosten aangaan.


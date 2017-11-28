---
title: aaaInstall Python en Hallo SDK - Azure
description: Meer informatie over hoe tooinstall Python en Hallo SDK toouse met Azure.
services: 
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: f36294be-daeb-4caf-9129-fce18130f552
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 09/06/2016
ms.author: lmazuel
ms.openlocfilehash: c1b394770f9abd3e654a23d79ae179a9af89e2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="installing-python-and-hello-sdk"></a><span data-ttu-id="5e6cd-103">Python en Hallo SDK installeren</span><span class="sxs-lookup"><span data-stu-id="5e6cd-103">Installing Python and hello SDK</span></span>
<span data-ttu-id="5e6cd-104">Python is eenvoudig tooset in Windows en is voorgeïnstalleerd op Mac, Linux, en [Bash voor Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="5e6cd-104">Python is easy tooset up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="5e6cd-105">Deze handleiding helpt u bij de installatie en het ophalen van de machine klaar voor gebruik met Azure.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-hello-python-azure-sdk"></a><span data-ttu-id="5e6cd-106">Wat is in hello Azure SDK voor Python?</span><span class="sxs-lookup"><span data-stu-id="5e6cd-106">What's in hello Python Azure SDK?</span></span>
<span data-ttu-id="5e6cd-107">Hello Azure SDK voor Python omvat onderdelen waarmee u toodevelop, implementeren en beheren van toepassingen voor Azure Python.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-107">hello Azure SDK for Python includes components that allow you toodevelop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="5e6cd-108">Hello Azure SDK voor Python bevat met name de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="5e6cd-108">Specifically, hello Azure SDK for Python includes hello following:</span></span>

* <span data-ttu-id="5e6cd-109">**Management-bibliotheken**.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-109">**Management libraries**.</span></span> <span data-ttu-id="5e6cd-110">Deze klassenbibliotheken bieden een interface met het beheren van een Azure-resources, zoals opslagaccounts, virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="5e6cd-111">**Runtime-bibliotheken**.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-111">**Runtime libraries**.</span></span> <span data-ttu-id="5e6cd-112">Deze klassenbibliotheken bieden een interface voor toegang tot Azure-functies, zoals opslag en service bus.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-toouse"></a><span data-ttu-id="5e6cd-113">Welke Python en welke versie toouse</span><span class="sxs-lookup"><span data-stu-id="5e6cd-113">Which Python and which version toouse</span></span>
<span data-ttu-id="5e6cd-114">Er zijn verschillende versies van Python interpreters beschikbaar - voorbeelden zijn:</span><span class="sxs-lookup"><span data-stu-id="5e6cd-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="5e6cd-115">CPython - Hallo standard en meest gebruikte Python-interpreter</span><span class="sxs-lookup"><span data-stu-id="5e6cd-115">CPython - hello standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="5e6cd-116">PyPy - tooCPython snelle, compatibele alternatieve implementatie</span><span class="sxs-lookup"><span data-stu-id="5e6cd-116">PyPy - fast, compliant alternative implementation tooCPython</span></span>
* <span data-ttu-id="5e6cd-117">IronPython - Python-interpreter die wordt uitgevoerd op .net/CLR</span><span class="sxs-lookup"><span data-stu-id="5e6cd-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="5e6cd-118">Jython - Python-interpreter die wordt uitgevoerd op Hallo virtuele Java-Machine</span><span class="sxs-lookup"><span data-stu-id="5e6cd-118">Jython - Python interpreter that runs on hello Java Virtual Machine</span></span>

<span data-ttu-id="5e6cd-119">**CPython** v2.7 of v3.3 + en PyPy 5.4.0 zijn getest en worden ondersteund voor hello Azure SDK voor Python.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for hello Python Azure SDK.</span></span>

## <a name="where-tooget-python"></a><span data-ttu-id="5e6cd-120">Waar tooget Python?</span><span class="sxs-lookup"><span data-stu-id="5e6cd-120">Where tooget Python?</span></span>
<span data-ttu-id="5e6cd-121">Er zijn verschillende manieren tooget CPython:</span><span class="sxs-lookup"><span data-stu-id="5e6cd-121">There are several ways tooget CPython:</span></span>

* <span data-ttu-id="5e6cd-122">Rechtstreeks vanuit [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="5e6cd-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="5e6cd-123">Van een betrouwbare distro zoals [www.continuum.io][www.continuum.io], [www.enthought.com] [ www.enthought.com] of [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="5e6cd-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="5e6cd-124">Het bouwen van bron!</span><span class="sxs-lookup"><span data-stu-id="5e6cd-124">Build from source!</span></span>

<span data-ttu-id="5e6cd-125">Tenzij u een specifieke reden hebt, wordt aangeraden Hallo eerste twee opties.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-125">Unless you have a specific need, we recommend hello first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="5e6cd-126">SDK-installatie op Windows, Linux en Mac OS (clientbibliotheken)</span><span class="sxs-lookup"><span data-stu-id="5e6cd-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="5e6cd-127">Als u Python geïnstalleerd hebt, kunt u pip tooinstall een bundel van alle Hallo clientbibliotheken in uw bestaande Python 2.7 of Python 3.3 +-omgeving.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-127">If you already have Python installed, you can use pip tooinstall a bundle of all hello client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="5e6cd-128">Hiermee downloadt u hello-pakketten van Hallo [Python Package Index] [ Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="5e6cd-128">This downloads hello packages from hello [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="5e6cd-129">Mogelijk moet u beheerdersrechten:</span><span class="sxs-lookup"><span data-stu-id="5e6cd-129">You may need administrator rights:</span></span>

* <span data-ttu-id="5e6cd-130">Linux- en Mac OS, gebruik Hallo `sudo` opdracht: `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-130">Linux and MacOS, use hello `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="5e6cd-131">Windows: open de PowerShell-opdracht met een opdrachtprompt als beheerder</span><span class="sxs-lookup"><span data-stu-id="5e6cd-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="5e6cd-132">U kunt afzonderlijk elke wisselaar voor elke Azure-service installeren:</span><span class="sxs-lookup"><span data-stu-id="5e6cd-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

<span data-ttu-id="5e6cd-133">Preview-pakketten kunnen worden geïnstalleerd met Hallo `--pre` vlag:</span><span class="sxs-lookup"><span data-stu-id="5e6cd-133">Preview packages can be installed using hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

<span data-ttu-id="5e6cd-134">U kunt ook een set van Azure-bibliotheken installeren op één regel met behulp van Hallo `azure` meta-pakket.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-134">You can also install a set of Azure libraries in a single line using hello `azure` meta-package.</span></span> <span data-ttu-id="5e6cd-135">Omdat niet alle pakketten in dit meta-pakket worden gepubliceerd als stabiel nog, Hallo `azure` meta-pakket is nog steeds in preview.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-135">Since not all packages in this meta-package are published as stable yet, hello `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="5e6cd-136">Echter, Hallo core pakketten vanuit code kwaliteit/volledigheid perspectieven kunnen worden overwogen 'stabiele' op dit moment</span><span class="sxs-lookup"><span data-stu-id="5e6cd-136">However, hello core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="5e6cd-137">het officiële label als zodanig synchroon met de andere talen zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="5e6cd-138">We hebben geen plannen op verdere grote wijzigingen tot die tijd.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="5e6cd-139">Omdat het is een preview-versie, moet u toouse hello `--pre` vlag:</span><span class="sxs-lookup"><span data-stu-id="5e6cd-139">Since it's a preview release, you need toouse hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="5e6cd-140">of rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="5e6cd-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="5e6cd-141">Meer pakketten ophalen</span><span class="sxs-lookup"><span data-stu-id="5e6cd-141">Getting More Packages</span></span>
<span data-ttu-id="5e6cd-142">Hallo [Python Package Index] [ Python Package Index] (PyPI) is een geavanceerde selectie van Python-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-142">hello [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="5e6cd-143">Als u een Distro tooinstall kiest, al hebt u de meeste Hallo interessante bits voor verschillende scenario's van web ontwikkeling tooTechnical Computing.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-143">If you chose tooinstall a Distro, you'll already have most of hello interesting bits for various scenarios from web development tooTechnical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="5e6cd-144">Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5e6cd-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="5e6cd-145">[Python-Tools voor Visual Studio][Python-Tools voor Visual Studio] (PTVS) is een gratis/OSS-invoegtoepassing van Microsoft die tegenover in een volwaardig Python IDE verandert:</span><span class="sxs-lookup"><span data-stu-id="5e6cd-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![How-naar-installatie-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="5e6cd-147">Met behulp van de PTVS is optioneel, maar wordt aanbevolen omdat dit u biedt ondersteuning voor Python en Web Project/oplossing, foutopsporing, profilering, interactieve venster, bewerken van sjablonen en Intellisense.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="5e6cd-148">PTVS maakt het ook eenvoudig toodeploy tooMicrosoft Azure, met ondersteuning voor de implementatie te[Cloudservices](cloud-services/cloud-services-python-ptvs.md) en [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="5e6cd-148">PTVS also makes it easy toodeploy tooMicrosoft Azure, with support for deployment too[Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="5e6cd-149">PTVS werkt met de bestaande installatie van Visual Studio 2013 of 2015 2017.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="5e6cd-150">Zie voor documentatie, downloads en discussies [Python-Tools voor Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="5e6cd-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="5e6cd-151">Python Azure scenario's voor Linux en Mac OS</span><span class="sxs-lookup"><span data-stu-id="5e6cd-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="5e6cd-152">Voor Linux- of Mac OS, belangrijkste Azure scenario's die worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="5e6cd-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="5e6cd-153">Azure-Services gebruiken met behulp van de clientbibliotheken Hallo voor Python</span><span class="sxs-lookup"><span data-stu-id="5e6cd-153">Consuming Azure Services by using hello client libraries for Python</span></span>
2. <span data-ttu-id="5e6cd-154">Uw app uitvoert in een virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="5e6cd-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="5e6cd-155">Ontwikkelen en tooAzure Websites publiceren met Git</span><span class="sxs-lookup"><span data-stu-id="5e6cd-155">Developing and publishing tooAzure Websites using Git</span></span>

<span data-ttu-id="5e6cd-156">Hallo eerste scenario kunt u tooauthor uitgebreide web-apps die van hello Azure PaaS-mogelijkheden, zoals gebruikmaken [blobopslag](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [opslag in de wachtrij](storage/queues/storage-python-how-to-use-queue-storage.md), [opslag tabel](cosmos-db/table-storage-how-to-use-python.md) enzovoort via Pythonic wrappers voor hello Azure REST API's.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-156">hello first scenario enables you tooauthor rich web apps that take advantage of hello Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for hello Azure REST APIs.</span></span> <span data-ttu-id="5e6cd-157">Deze identiek werken op Windows, Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="5e6cd-158">U kunt ook deze clientbibliotheken gebruiken vanuit uw lokale ontwikkelcomputer of een Linux-VM uitgevoerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="5e6cd-159">Hallo VM scenario u gewoon een Linux-VM van uw keuze (Ubuntu, CentOS, Suse) starten en uitvoeren of beheren wat u leuk.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-159">For hello VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="5e6cd-160">Een voorbeeld: u kunt uitvoeren [IPython] [ IPython] REPL/laptop op uw Windows-Mac/Linux-machine en het punt uw browser tooa Linux of Windows multi-proc VM uitgevoerd Hallo IPython-Engine op Azure.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser tooa Linux or Windows multi-proc VM running hello IPython Engine on Azure.</span></span>

<span data-ttu-id="5e6cd-161">Voor meer informatie over tooset up van een Linux-VM Zie Hallo [maken van een virtuele Machine waarop Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-161">For information on how tooset up a Linux VM, see hello [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="5e6cd-162">Git-implementatie gebruikt, kunt u een Python-webtoepassing ontwikkelen en publiceren tooan Azure-Website op een ander besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-162">Using Git deployment, you can develop a Python web application and publish it tooan Azure Website from any operating system.</span></span>  <span data-ttu-id="5e6cd-163">Wanneer u uw tooAzure opslagplaats pushen, maakt automatisch een virtuele omgeving en pip installeert de vereiste pakketten.</span><span class="sxs-lookup"><span data-stu-id="5e6cd-163">When you push your repository tooAzure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="5e6cd-164">Zie voor meer informatie over het ontwerpen en publiceren van Azure Websites Hallo-zelfstudies voor [Websites maken met Django](app-service-web/web-sites-python-create-deploy-django-app.md), [maken van Websites met Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), en [maken van Websites met Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="5e6cd-164">For more information on developing and publishing Azure Websites, see hello tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="5e6cd-165">Zie voor meer algemene informatie over het gebruik van elk WSGI compatibel framework [Python configureren met Azure Websites](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5e6cd-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="5e6cd-166">Aanvullende Software en Resources:</span><span class="sxs-lookup"><span data-stu-id="5e6cd-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="5e6cd-167">Azure SDK voor Python ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="5e6cd-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="5e6cd-168">Azure SDK voor Python GitHub</span><span class="sxs-lookup"><span data-stu-id="5e6cd-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="5e6cd-169">Officiële Azure-voorbeelden voor Python</span><span class="sxs-lookup"><span data-stu-id="5e6cd-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="5e6cd-170">[Continue Analytics Python-distributie][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="5e6cd-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="5e6cd-171">[Enthought Python-distributie][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="5e6cd-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="5e6cd-172">[ActiveState Python-distributie][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="5e6cd-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="5e6cd-173">[SciPy - een suite van wetenschappelijke Python-bibliotheken][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="5e6cd-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="5e6cd-174">[NumPy - een bibliotheek cijfers voor Python][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="5e6cd-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="5e6cd-175">[Django-Project - een framework volwassen web/CMS][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="5e6cd-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="5e6cd-176">[IPython - een geavanceerde REPL/laptop voor Python][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="5e6cd-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="5e6cd-177">[Python-Tools voor Visual Studio op GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="5e6cd-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="5e6cd-178">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="5e6cd-178">Python Developer Center</span></span>](/develop/python/)

[Continuum Analytics Python Distribution]: http://continuum.io
[Enthought Python Distribution]: http://www.enthought.com
[ActiveState Python Distribution]: http://www.activestate.com
[www.python.org]: http://www.python.org
[www.continuum.io]: http://continuum.io
[www.enthought.com]: http://www.enthought.com
[www.activestate.com]: http://www.activestate.com
[SciPy - A suite of Scientific Python libraries]: http://www.scipy.org
[NumPy - A numerics library for Python]: http://www.numpy.org
[Django Project - A mature web framework/CMS]: http://www.djangoproject.com
[IPython - an advanced REPL/Notebook for Python]: http://ipython.org
[IPython]: http://ipython.org
[IPython Notebook on Azure]: virtual-machines-linux-jupyter-notebook.md
[Cloud Services]: cloud-services-python-ptvs.md
[Websites]: web-sites-python-ptvs-django-mysql.md
[Python-Tools voor Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio on GitHub]: https://github.com/microsoft/ptvs
[Python Package Index]: http://pypi.python.org/pypi
[Microsoft Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?LinkId=254281
[Microsoft Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?LinkID=516990
[Setting up a Linux VM via hello Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How toouse hello Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md

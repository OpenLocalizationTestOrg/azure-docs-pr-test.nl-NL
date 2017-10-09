---
title: een laptop van een Jupyter/IPython aaaCreate | Microsoft Docs
description: Meer informatie over hoe toodeploy hello Jupyter/IPython laptop op een virtuele Linux-machine gemaakt met de Hallo resource manager-implementatiemodel in Azure.
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="ce78b-103">Een Azure VM Jupyter installeren en uitvoeren van een Jupyter-Notebook in Azure maken</span><span class="sxs-lookup"><span data-stu-id="ce78b-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="ce78b-104">Hallo [Jupyter project](http://jupyter.org), voorheen Hallo [IPython project](http://ipython.org), bevat een verzameling van hulpprogramma's voor wetenschappelijke berekeningen met behulp van krachtige interactieve shells die met Hallo maken van de uitvoering van code combineren een live rekenkundige document.</span><span class="sxs-lookup"><span data-stu-id="ce78b-104">hello [Jupyter project](http://jupyter.org), formerly hello [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with hello creation of a live computational document.</span></span> <span data-ttu-id="ce78b-105">Deze bestanden notebook mag willekeurige tekst, rekenkundige formules, invoer code, resultaten, afbeeldingen, video's en een ander type media dat een moderne webbrowser is in staat om weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ce78b-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="ce78b-106">Hiermee wordt aangegeven of u bent helemaal nieuwe tooPython en toolearn wilt in een plezier, interactieve omgeving of komen een aantal ernstige parallel/technische computing, Hallo Jupyter-Notebook is een uitstekende keuze.</span><span class="sxs-lookup"><span data-stu-id="ce78b-106">Whether you're absolutely new tooPython and want toolearn it in a fun, interactive environment or do some serious parallel/technical computing, hello Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="ce78b-107">![Schermopname](./media/jupyter-notebook/ipy-notebook-spectral.png) met behulp van SciPy en Matplotlib pakketten tooanalyze Hallo structuur van het opnemen van een geluid.</span><span class="sxs-lookup"><span data-stu-id="ce78b-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages tooanalyze hello structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="ce78b-108">Jupyter twee manieren: De Azure-laptops of aangepaste implementatie</span><span class="sxs-lookup"><span data-stu-id="ce78b-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="ce78b-109">Azure biedt een service die u kunt ook gebruiken[snel starten met Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce78b-109">Azure provides a service that you can use too[quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="ce78b-110">Met behulp van hello Azure Notebook Service, kunt u eenvoudig toegankelijk is via het web interface toegang tooJupyter van toegang tot schaalbare rekenkundige resources met alle Hallo stroom van Python en bijbehorende veel bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="ce78b-110">By using hello Azure Notebook Service, you can easily gain access tooJupyter's web-accessible interface to scalable computational resources with all hello power of Python and its many libraries.</span></span>  <span data-ttu-id="ce78b-111">Omdat het Hallo-installatie wordt verwerkt door het Hallo-service, kunnen gebruikers toegang tot deze bronnen zonder dat nodig is voor beheer en configuratie door gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ce78b-111">Since hello installation is handled by hello service, users can access these resources without hello need for administration and configuration by hello user.</span></span>

<span data-ttu-id="ce78b-112">Als het Hallo-notebook service werkt niet voor uw scenario blijven tooread in dit artikel die wordt leert u hoe toodeploy Hallo Jupyter-Notebook in Microsoft Azure met behulp van de virtuele Linux-machines (VM's).</span><span class="sxs-lookup"><span data-stu-id="ce78b-112">If hello notebook service does not work for your scenario please continue tooread this article which will will show you how toodeploy hello Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="ce78b-113">Maken en configureren van een virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="ce78b-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="ce78b-114">de eerste stap Hallo toocreate is een virtuele machine (VM) uitgevoerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="ce78b-114">hello first step is toocreate a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="ce78b-115">Deze virtuele machine is een volledig besturingssysteem in de cloud Hallo en wordt gebruikt voor het uitvoeren van Hallo Jupyter-Notebook.</span><span class="sxs-lookup"><span data-stu-id="ce78b-115">This VM is a complete operating system in hello cloud and will be used to run hello Jupyter Notebook.</span></span> <span data-ttu-id="ce78b-116">Azure is geschikt voor Linux- en Windows virtuele machines worden uitgevoerd en wordt ingegaan op het Hallo-installatie van Jupyter op beide typen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="ce78b-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover hello setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="ce78b-117">Maak een Linux-VM en openen van een poort voor Jupyter</span><span class="sxs-lookup"><span data-stu-id="ce78b-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="ce78b-118">Volg de instructies Hallo [hier] [ portal-vm-linux] toocreate een virtuele machine Hallo *Ubuntu* distributie.</span><span class="sxs-lookup"><span data-stu-id="ce78b-118">Follow hello instructions given [here][portal-vm-linux] toocreate a virtual machine of hello *Ubuntu* distribution.</span></span> <span data-ttu-id="ce78b-119">Ubuntu Server 14.04 TNS maakt gebruik van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ce78b-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="ce78b-120">We gaan ervan uit dat de gebruikersnaam Hallo *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="ce78b-120">We'll assume hello user name *azureuser*.</span></span>

<span data-ttu-id="ce78b-121">Nadat Hallo virtuele machine wordt geïmplementeerd, moeten we tooopen van een beveiligingsregel voor op Hallo netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="ce78b-121">After hello virtual machine deploys we need tooopen up a security rule on hello network security group.</span></span>  <span data-ttu-id="ce78b-122">Hallo Azure-portal, ga te**Netwerkbeveiligingsgroepen** en open Hallo tabblad voor Hallo beveiligingsgroep bijbehorende tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="ce78b-122">From hello Azure portal, go too**Network Security Groups** and open hello tab for hello Security Group corresponding tooyour VM.</span></span> <span data-ttu-id="ce78b-123">Moet u een inkomende beveiligingsregel tooadd Hello volgende instellingen: **TCP** voor Hallo-protocol,  **\***  voor Hallo bronpoort (openbaar) en **9999** voor Hallo-doelpoort (particuliere).</span><span class="sxs-lookup"><span data-stu-id="ce78b-123">You need tooadd an Inbound Security rule with hello following settings: **TCP** for hello protocol, **\*** for hello source (public) port and **9999** for hello destination (private) port.</span></span>

![schermopname](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="ce78b-125">In de beveiligingsgroep van uw netwerk, klikt u op **netwerkinterfaces** en Opmerking Hallo **openbaar IP-adres** zoals het benodigde tooconnect tooyour VM in de volgende stap Hallo zal zijn.</span><span class="sxs-lookup"><span data-stu-id="ce78b-125">While in your Network Security Group, click on **Network Interfaces** and note hello **Public IP Address** as it will be needed tooconnect tooyour VM in hello next step.</span></span>

## <a name="install-required-software-on-hello-vm"></a><span data-ttu-id="ce78b-126">Vereiste software installeren op Hallo VM</span><span class="sxs-lookup"><span data-stu-id="ce78b-126">Install required software on hello VM</span></span>
<span data-ttu-id="ce78b-127">toorun Hallo Jupyter-Notebook op de virtuele machine, moet we eerst Jupyter en de bijbehorende afhankelijkheden installeren.</span><span class="sxs-lookup"><span data-stu-id="ce78b-127">toorun hello Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="ce78b-128">Verbind tooyour linux vm die gebruikmaakt van ssh en Hallo gebruikersnaam en wachtwoord paar die u hebt gekozen tijdens het maken van Hallo vm.</span><span class="sxs-lookup"><span data-stu-id="ce78b-128">Connect tooyour linux vm using ssh and hello username/password pair you chose when you created hello vm.</span></span> <span data-ttu-id="ce78b-129">In deze zelfstudie wordt u met PuTTY en verbinding maken vanaf Windows.</span><span class="sxs-lookup"><span data-stu-id="ce78b-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="ce78b-130">Jupyter op Ubuntu installeren</span><span class="sxs-lookup"><span data-stu-id="ce78b-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="ce78b-131">Installeer Anaconda, een populaire gegevens wetenschappelijke python-distributie met behulp van een Hallo koppelingen van [continue Analytics](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="ce78b-131">Install Anaconda, a popular data science python distribution, using one of hello links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="ce78b-132">Hallo onderstaande koppelingen zijn op Hallo moment van schrijven van dit document, Hallo meest up toodate versies.</span><span class="sxs-lookup"><span data-stu-id="ce78b-132">As of hello writing of this document, hello below links are hello most up toodate versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="ce78b-133">Anaconda installeert voor Linux</span><span class="sxs-lookup"><span data-stu-id="ce78b-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="ce78b-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="ce78b-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="ce78b-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="ce78b-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="ce78b-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64-bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="ce78b-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="ce78b-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64-bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="ce78b-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce78b-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32-bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="ce78b-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="ce78b-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32-bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="ce78b-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="ce78b-140">Installeren van Anaconda3 2.3.0 64-bits op Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ce78b-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="ce78b-141">Een voorbeeld: dit is hoe u Anaconda op Ubuntu kunt installeren</span><span class="sxs-lookup"><span data-stu-id="ce78b-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![schermopname](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="ce78b-143">Jupyter configureren en gebruiken van SSL</span><span class="sxs-lookup"><span data-stu-id="ce78b-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="ce78b-144">Na de installatie moet tootake een moment toosetup Hallo-configuratiebestanden voor Jupyter.</span><span class="sxs-lookup"><span data-stu-id="ce78b-144">After installing we need tootake a moment toosetup hello configuration files for Jupyter.</span></span> <span data-ttu-id="ce78b-145">Als u dreigen bij het configureren van Jupyter ervaart mogelijk handig toolook op Hallo [Jupyter-documentatie voor het uitvoeren van een Server Notebook](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="ce78b-145">If you experience troubles with configuring Jupyter it may be helpful toolook at hello [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="ce78b-146">Volgende we `cd` toohello directory toocreate onze SSL-certificaat profiel en Hallo profielen configuratiebestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="ce78b-146">Next we `cd` toohello profile directory toocreate our SSL certificate and edit hello profiles configuration file.</span></span>

<span data-ttu-id="ce78b-147">Gebruik Hallo volgende opdracht op Linux.</span><span class="sxs-lookup"><span data-stu-id="ce78b-147">On Linux use hello following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="ce78b-148">Gebruik Hallo opdracht toocreate Hallo SSL-certificaat (Linux en Windows) te volgen.</span><span class="sxs-lookup"><span data-stu-id="ce78b-148">Use hello following command toocreate hello SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="ce78b-149">Houd er rekening mee dat omdat u een zelfondertekend SSL-certificaat, wanneer u verbinding maakt toohello notebook uw browser u een beveiligingswaarschuwing weergegeven krijgt.</span><span class="sxs-lookup"><span data-stu-id="ce78b-149">Note that since we are creating a self-signed SSL certificate, when connecting toohello notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="ce78b-150">Voor gebruik in productieomgevingen op lange termijn zult u toouse een correct ondertekend certificaat dat is gekoppeld aan uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="ce78b-150">For long-term production use, you will want toouse a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="ce78b-151">Aangezien Certificaatbeheer buiten bereik van deze demo hello is, wordt er tooa zelf-ondertekend certificaat stick nu.</span><span class="sxs-lookup"><span data-stu-id="ce78b-151">Since certificate management is beyond hello scope of this demo, we will stick tooa self-signed certificate for now.</span></span>

<span data-ttu-id="ce78b-152">Bovendien toousing een certificaat, moet u ook opgeven een wachtwoord tooprotect uw laptop tegen onbevoegd gebruik.</span><span class="sxs-lookup"><span data-stu-id="ce78b-152">In addition toousing a certificate, you must also provide a password tooprotect your notebook from unauthorized use.</span></span>  <span data-ttu-id="ce78b-153">Uit veiligheidsoverwegingen Jupyter versleutelde wachtwoorden in het configuratiebestand, dus u tooencrypt moet uw wachtwoord wordt gebruikt eerst.</span><span class="sxs-lookup"><span data-stu-id="ce78b-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need tooencrypt your password first.</span></span>  <span data-ttu-id="ce78b-154">IPython biedt een hulpprogramma toodo Hallo volgende opdracht achter de opdrachtprompt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ce78b-154">IPython provides a utility toodo so; at a command prompt run hello following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="ce78b-155">Dit wordt u gevraagd om een wachtwoord en de bevestiging en wordt vervolgens Hallo wachtwoord afdrukken.</span><span class="sxs-lookup"><span data-stu-id="ce78b-155">This will prompt you for a password and confirmation, and will then print hello password.</span></span> <span data-ttu-id="ce78b-156">Let op Hallo stap</span><span class="sxs-lookup"><span data-stu-id="ce78b-156">Note this for hello following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

<span data-ttu-id="ce78b-157">Vervolgens bewerken we configuratiebestand Hallo-profiel, wat de `jupyter_notebook_config.py` in Hallo-map in.</span><span class="sxs-lookup"><span data-stu-id="ce78b-157">Next, we will edit hello profile's configuration file, which is the `jupyter_notebook_config.py` file in hello directory you are in.</span></span>  <span data-ttu-id="ce78b-158">Opmerking dat dit bestand bestaat mogelijk niet--alleen maken als dit Hallo geval is.</span><span class="sxs-lookup"><span data-stu-id="ce78b-158">Note that this file may not exist -- just create it if that is hello case.</span></span>  <span data-ttu-id="ce78b-159">Dit bestand heeft een aantal velden en standaard alle zijn opgenomen als opmerkingen.  U kunt dit bestand openen in een teksteditor openen van uw eigen smaak en moet u ervoor zorgen dat deze ten minste heeft Hallo volgende inhoud.</span><span class="sxs-lookup"><span data-stu-id="ce78b-159">This file has a number of fields and by default all are commented out.  You can open this file with any text editor of your liking, and you should ensure that it has at least hello following content.</span></span> <span data-ttu-id="ce78b-160">**Ervoor tooreplace hello c.NotebookApp.password in de configuratie met Hallo sha1 uit de vorige stap Hallo Hallo worden**.</span><span class="sxs-lookup"><span data-stu-id="ce78b-160">**Be sure tooreplace hello c.NotebookApp.password in hello config with hello sha1 from hello previous step**.</span></span>

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a><span data-ttu-id="ce78b-161">Hallo Jupyter-Notebook uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ce78b-161">Run hello Jupyter Notebook</span></span>
<span data-ttu-id="ce78b-162">We zijn nu gereed toostart hello Jupyter-Notebook.</span><span class="sxs-lookup"><span data-stu-id="ce78b-162">At this point we are ready toostart hello Jupyter Notebook.</span></span> <span data-ttu-id="ce78b-163">toodo, toohello directory toostore notitieblokken in en start Hallo Jupyter-Notebook server met volgende opdracht Hallo navigeren.</span><span class="sxs-lookup"><span data-stu-id="ce78b-163">toodo this, navigate toohello directory you want toostore notebooks in and start hello Jupyter Notebook server with hello following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="ce78b-164">U moet nu worden kunnen tooaccess uw Jupyter-Notebook op Hallo adres `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="ce78b-164">You should now be able tooaccess your Jupyter Notebook at hello address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="ce78b-165">Wanneer u uw laptop voor het eerst opent, wordt de Hallo-aanmeldingspagina om uw wachtwoord gevraagd.</span><span class="sxs-lookup"><span data-stu-id="ce78b-165">When you first access your notebook, hello login page asks for your password.</span></span> <span data-ttu-id="ce78b-166">En wanneer u zich aanmeldt, ziet u Hallo 'Jupyter-Notebook Dashboard', die het center ontrole voor alle bewerkingen van de laptop is.</span><span class="sxs-lookup"><span data-stu-id="ce78b-166">And once you log in, you will see hello "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="ce78b-167">U kunt via deze pagina nieuwe notitieblokken maken en bestaande bestanden te openen.</span><span class="sxs-lookup"><span data-stu-id="ce78b-167">From this page you can create new notebooks and open existing ones.</span></span>

![schermopname](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a><span data-ttu-id="ce78b-169">Met behulp van Hallo Jupyter-Notebook</span><span class="sxs-lookup"><span data-stu-id="ce78b-169">Using hello Jupyter Notebook</span></span>
<span data-ttu-id="ce78b-170">Als u klikt op Hallo **nieuw** knop klikt, ziet u Hallo openingspagina te volgen.</span><span class="sxs-lookup"><span data-stu-id="ce78b-170">If you click hello **New** button, you will see hello following opening page.</span></span>

![schermopname](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="ce78b-172">Hallo gebied gemarkeerd met een `In []:` vragen invoergebied hello, en kunt u hier geldige Python-code invoeren en deze wordt uitgevoerd als u raakt `Shift-Enter` of klik op het pictogram Hallo 'Afspelen' (Hallo rechts driehoek op Hallo werkbalk).</span><span class="sxs-lookup"><span data-stu-id="ce78b-172">hello area marked with an `In []:` prompt is hello input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on hello "Play" icon (hello right-pointing triangle in hello toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="ce78b-173">Een krachtige paradigma: live rekenkundige documenten met uitgebreide media</span><span class="sxs-lookup"><span data-stu-id="ce78b-173">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="ce78b-174">Hallo-notebook zelf erop vertrouwen dat logisch tooanyone die heeft gebruikt Python en een tekstverwerker, omdat deze zich in een aantal manieren een combinatie van beide: blokken Python-code kan worden uitgevoerd, maar u kunt ook opmerkingen en andere tekst houden door te wijzigen van de stijl van een cel vanuit 'Code' Hallo 'Ma rkdown' hello vervolgkeuzelijst met op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="ce78b-174">hello notebook itself should feel very natural tooanyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing hello style of a cell from "Code" too"Markdown" using hello drop-down menu in the toolbar.</span></span>

<span data-ttu-id="ce78b-175">Jupyter nog veel meer dan een tekstverwerkingsprogramma zoals kunt u de combinatie van berekening en rijke media (tekst, afbeeldingen, video en vrijwel alles die een moderne webbrowser kunt weergeven).</span><span class="sxs-lookup"><span data-stu-id="ce78b-175">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="ce78b-176">U kunt combineren, tekst, code, video's en meer!</span><span class="sxs-lookup"><span data-stu-id="ce78b-176">You can mix, text, code, videos and more!</span></span>

![schermopname](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="ce78b-178">En met Hallo kracht van Python van veel uitstekende bibliotheken voor technische en wetenschappelijke computergebruik in Hallo volgende schermafdruk is een eenvoudige berekening Hello dezelfde als een analyse complexe netwerk in een omgeving vereenvoudigen kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ce78b-178">And with hello power of Python's many excellent libraries for scientific and technical computing, in hello following screenshot, a simple calculation can be performed with hello same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="ce78b-179">Dit paradigma van Hallo power van moderne web Hallo combineren met live berekening biedt veel mogelijkheden en is ideaal voor cloud Hallo; Hallo Notebook kan worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="ce78b-179">This paradigm of mixing hello power of hello modern web with live computation offers many possibilities, and is ideally suited for hello cloud; hello Notebook can be used:</span></span>

* <span data-ttu-id="ce78b-180">Als een rekenkundige Kladblok toorecord experimentele werken op een probleem.</span><span class="sxs-lookup"><span data-stu-id="ce78b-180">As a computational scratchpad toorecord exploratory work on a problem.</span></span>
* <span data-ttu-id="ce78b-181">tooshare resulteert met collega's, 'live' rekenkundige vorm of in papier indelingen (HTML-, PDF-bestand).</span><span class="sxs-lookup"><span data-stu-id="ce78b-181">tooshare results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="ce78b-182">toodistribute aanwezig live lesmateriaal die betrekking hebben op berekening, zodat studenten onmiddellijk met echte code hello experimenteren kunnen, wijzigen en opnieuw interactief uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ce78b-182">toodistribute and present live teaching materials that involve computation, so students can immediately experiment with hello real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="ce78b-183">tooprovide 'uitvoerbare papier' hello resultaten van onderzoek aanwezig zijn op een manier die direct kan worden gereproduceerd, gevalideerd en uitgebreid door anderen.</span><span class="sxs-lookup"><span data-stu-id="ce78b-183">tooprovide "executable papers" that present hello results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="ce78b-184">Als een platform voor samenwerking computing: meerdere gebruikers kunnen zich aanmelden in toothe dezelfde notebook server tooshare een live rekenkundige sessie.</span><span class="sxs-lookup"><span data-stu-id="ce78b-184">As a platform for collaborative computing: multiple users can log in toothe same notebook server tooshare a live computational session.</span></span>

<span data-ttu-id="ce78b-185">Wanneer u toohello IPython broncode gaat [opslagplaats][repository], vindt u een hele map met notebook voorbeelden die u kunt downloaden en vervolgens experimenteren met op uw eigen Jupyter Azure VM.</span><span class="sxs-lookup"><span data-stu-id="ce78b-185">If you go toohello IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="ce78b-186">Gewoon downloaden Hallo `.ipynb` bestanden van Hallo site en uploaden naar Hallo dashboard van uw laptop virtuele machine van Azure (of deze rechtstreeks in VM Hallo downloaden).</span><span class="sxs-lookup"><span data-stu-id="ce78b-186">Simply download hello `.ipynb` files from hello site and upload them onto hello dashboard of your notebook Azure VM (or download them directly into hello VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="ce78b-187">Conclusie</span><span class="sxs-lookup"><span data-stu-id="ce78b-187">Conclusion</span></span>
<span data-ttu-id="ce78b-188">Hallo Jupyter-Notebook biedt een krachtige interface voor toegang tot interactief Hallo power van Hallo Python-ecosysteem in Azure.</span><span class="sxs-lookup"><span data-stu-id="ce78b-188">hello Jupyter Notebook provides a powerful interface for accessing interactively hello power of hello Python ecosystem on Azure.</span></span>  <span data-ttu-id="ce78b-189">Er wordt een breed scala aan gebruik gevallen, met inbegrip van eenvoudige exploratie en leren Python, data-analyse en visualisatie, simulatie en parallelle berekeningen aangegeven.</span><span class="sxs-lookup"><span data-stu-id="ce78b-189">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="ce78b-190">Hallo resulterende Notebook documenten bevatten een volledig overzicht van Hallo berekeningen die worden uitgevoerd en kunnen worden gedeeld met andere Jupyter-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="ce78b-190">hello resulting Notebook documents contain a complete record of hello computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="ce78b-191">Hallo Jupyter-Notebook kan worden gebruikt als een lokale toepassing, maar dit is ideaal voor cloudimplementaties op Azure</span><span class="sxs-lookup"><span data-stu-id="ce78b-191">hello Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="ce78b-192">Hallo kernfuncties van Jupyter zijn ook beschikbaar in Visual Studio via de [Python-Tools voor Visual Studio] [ Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="ce78b-192">hello core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="ce78b-193">PTVS is een gratis en open-source-invoegtoepassing van Microsoft Visual Studio in een geavanceerde Python-ontwikkelomgeving waarin een geavanceerde editor met IntelliSense foutopsporing, verandert profileringsoptimalisaties en parallelle berekeningen integratie.</span><span class="sxs-lookup"><span data-stu-id="ce78b-193">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce78b-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ce78b-194">Next steps</span></span>
<span data-ttu-id="ce78b-195">Zie voor meer informatie, Hallo [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="ce78b-195">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs

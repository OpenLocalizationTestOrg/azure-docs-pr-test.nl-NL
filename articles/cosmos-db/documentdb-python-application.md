---
title: aaaPython Flask web application zelfstudie voor Azure Cosmos DB | Microsoft Docs
description: Bekijk een databasezelfstudie over het gebruik van Azure DB die Cosmos toostore en toegang tot gegevens uit een Python Flask-webtoepassing gehost op Azure. Oplossingen voor het ontwikkelen van toepassingen zoeken.
keywords: Toepassingsontwikkeling, python flask, python-webtoepassing, python-webontwikkeling
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="4f6d8-105">Een Python Flask-webtoepassing bouwen met Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4f6d8-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f6d8-106">.NET</span><span class="sxs-lookup"><span data-stu-id="4f6d8-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="4f6d8-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="4f6d8-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="4f6d8-108">Java</span><span class="sxs-lookup"><span data-stu-id="4f6d8-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="4f6d8-109">Python</span><span class="sxs-lookup"><span data-stu-id="4f6d8-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="4f6d8-110">Deze zelfstudie leert u hoe toouse Azure Cosmos DB toostore en toegang tot gegevens uit een Python-webtoepassing gehost op Azure en wordt ervan uitgegaan dat u hebt enige ervaring met behulp van Python en Azure websites.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-110">This tutorial shows you how toouse Azure Cosmos DB toostore and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="4f6d8-111">In deze zelfstudie komen de volgende onderwerpen aan bod:</span><span class="sxs-lookup"><span data-stu-id="4f6d8-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="4f6d8-112">Maken en inrichten van een Cosmos-DB-account.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="4f6d8-113">Maken van een Python Flask-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="4f6d8-114">Verbinding maken met behulp van de Cosmos-DB van uw webtoepassing tooand.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-114">Connecting tooand using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="4f6d8-115">Hallo web application tooAzure wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-115">Deploying hello web application tooAzure.</span></span>

<span data-ttu-id="4f6d8-116">Door deze zelfstudie te volgen, bouwt u een eenvoudige stemtoepassing waarmee u toovote voor een poll.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-116">By following this tutorial, you will build a simple voting application that allows you toovote for a poll.</span></span>

![Schermopname van het Hallo-stemtoepassing is gemaakt met deze databasezelfstudie](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="4f6d8-118">Vereisten voor de databasezelfstudie</span><span class="sxs-lookup"><span data-stu-id="4f6d8-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="4f6d8-119">Voordat u Hallo-instructies in dit artikel uitvoert, moet u ervoor zorgen dat er Hallo volgende zijn geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="4f6d8-119">Before following hello instructions in this article, you should ensure that you have hello following installed:</span></span>

* <span data-ttu-id="4f6d8-120">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-120">An active Azure account.</span></span> <span data-ttu-id="4f6d8-121">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4f6d8-122">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="4f6d8-123">OF</span><span class="sxs-lookup"><span data-stu-id="4f6d8-123">OR</span></span> 

    <span data-ttu-id="4f6d8-124">Een lokale installatie van Hallo [Azure Cosmos DB Emulator](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="4f6d8-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="4f6d8-126">[Python-Tools voor Visual Studio](https://github.com/Microsoft/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="4f6d8-127">[Microsoft Azure SDK voor Python 2.7](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="4f6d8-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4f6d8-129">Als u Python 2.7 voor Hallo eerst installeert, zorg ervoor dat in het welkomstscherm aanpassen Python 2.7.13, u selecteert **python.exe tooPath toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-129">If you are installing Python 2.7 for hello first time, ensure that in hello Customize Python 2.7.13 screen, you select **Add python.exe tooPath**.</span></span>
> 
> ![Schermopname van het welkomstscherm van aanpassen Python 2.7.11, waar u tooselect Add python.exe tooPath nodig](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="4f6d8-131">[Microsoft Visual C++ Compiler voor Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="4f6d8-132">Stap 1: een Azure Cosmos DB-databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="4f6d8-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="4f6d8-133">Begin met het maken van een Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="4f6d8-134">Als u al een account hebt of als u Azure Cosmos DB Emulator Hallo voor deze zelfstudie, kunt u overslaan te[stap 2: Maak een nieuwe Python Flask-webtoepassing](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-134">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="4f6d8-135">Er wordt nu zien hoe een nieuwe Python Flask-toepassing hello toocreate up gemalen.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-135">We will now walk through how toocreate a new Python Flask web application from hello ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="4f6d8-136">Stap 2: een nieuwe Python Flask-webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="4f6d8-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="4f6d8-137">In Visual Studio op Hallo **bestand** menu te verwijzen**nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-137">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="4f6d8-138">Hallo **nieuw Project** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-138">hello **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="4f6d8-139">Vouw in het linkerdeelvenster hello, **sjablonen** en vervolgens **Python**, en klik vervolgens op **Web**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-139">In hello left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="4f6d8-140">Selecteer **Flask-webproject** in het middelste deelvenster Hallo en klik vervolgens in Hallo **naam** vak type **zelfstudie**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-140">Select **Flask  Web Project** in hello center pane, then in hello **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="4f6d8-141">Houd er rekening mee dat Python-pakketnamen alleen kleine letters bevatten, zijn moeten zoals beschreven in Hallo [stijlgids voor Python-Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-141">Remember that Python package names should be all lowercase, as described in hello [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="4f6d8-142">Voor deze nieuwe tooPython Flask is een ontwikkelframework voor webtoepassingen waarmee u sneller webtoepassingen in Python bouwen.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-142">For those new tooPython Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Schermopname van het venster van de Hallo-nieuw Project in Visual Studio met Python gemarkeerd op Hallo links, Python Flask-webproject is geselecteerd in Hallo midden en Hallo naam tutorial in het naamvak Hallo](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="4f6d8-144">In Hallo **Python-Tools voor Visual Studio** venster, klikt u op **installeren in een virtuele omgeving**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-144">In hello **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Schermopname van het Hallo-databasezelfstudie - Python-Tools voor Visual Studio-venster](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="4f6d8-146">In Hallo **virtuele omgeving toevoegen** venster kunt u Hallo standaardinstellingen accepteren en Python 2.7 als basisomgeving hello gebruiken, omdat PyDocumentDB biedt momenteel geen ondersteuning voor Python 3.x en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-146">In hello **Add Virtual Environment** window, you can accept hello defaults and use Python 2.7 as hello base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="4f6d8-147">Hiermee stelt u Hallo vereiste virtuele Python-omgeving voor uw project.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-147">This sets up hello required Python virtual environment for your project.</span></span>
   
    ![Schermopname van het Hallo-databasezelfstudie - Python-Tools voor Visual Studio-venster](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="4f6d8-149">Hallo venster uitvoer `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` wanneer Hallo-omgeving is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-149">hello output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when hello environment is successfully installed.</span></span>

## <a name="step-3-modify-hello-python-flask-web-application"></a><span data-ttu-id="4f6d8-150">Stap 3: Hallo Python Flask-webtoepassing wijzigen</span><span class="sxs-lookup"><span data-stu-id="4f6d8-150">Step 3: Modify hello Python Flask web application</span></span>
### <a name="add-hello-python-flask-packages-tooyour-project"></a><span data-ttu-id="4f6d8-151">Hallo Python Flask-pakketten tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="4f6d8-151">Add hello Python Flask packages tooyour project</span></span>
<span data-ttu-id="4f6d8-152">Nadat uw project is ingesteld, moet u tooadd Hallo vereiste Flask-pakketten tooyour project, inclusief pydocumentdb, Hallo Python-pakket voor DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-152">After your project is set up, you'll need tooadd hello required Flask packages tooyour project, including pydocumentdb, hello Python package for DocumentDB.</span></span>

1. <span data-ttu-id="4f6d8-153">Open in Solution Explorer Hallo-bestand met de naam **requirements.txt** en vervang Hallo inhoud door Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="4f6d8-153">In Solution Explorer, open hello file named **requirements.txt** and replace hello contents with hello following:</span></span>
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. <span data-ttu-id="4f6d8-154">Hallo opslaan **requirements.txt** bestand.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-154">Save hello **requirements.txt** file.</span></span> 
3. <span data-ttu-id="4f6d8-155">Klik in Solution Explorer met de rechtermuisknop op **env** en klik op **Install from requirements.txt** (Installeren vanuit requirements.txt).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Schermopname waarin env (Python 2.7) met installeren vanuit requirements.txt gemarkeerd in de lijst Hallo geselecteerd](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="4f6d8-157">Na de installatie is voltooid wordt het uitvoervenster Hallo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="4f6d8-157">After successful installation, hello output window displays hello following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="4f6d8-158">In zeldzame gevallen ziet u mogelijk een fout in het uitvoervenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-158">In rare cases, you might see a failure in hello output window.</span></span> <span data-ttu-id="4f6d8-159">Als dit gebeurt, Controleer of Hallo fout gerelateerde toocleanup.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-159">If this happens, check if hello error is related toocleanup.</span></span> <span data-ttu-id="4f6d8-160">Soms Hallo opschonen mislukt, maar Hallo-installatie is nog steeds geslaagd (omhoog schuiven in Hallo uitvoer venster tooverify dit).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-160">Sometimes hello cleanup fails, but hello installation will still be successful (scroll up in hello output window tooverify this).</span></span> <span data-ttu-id="4f6d8-161">U kunt uw installatie controleren door [controleren Hallo virtuele omgeving](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-161">You can check your installation by [Verifying hello virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="4f6d8-162">Als het Hallo-installatie is mislukt, maar Hallo controle is geslaagd, is het OK toocontinue.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-162">If hello installation failed but hello verification is successful, it's OK toocontinue.</span></span>
   > 
   > 

### <a name="verify-hello-virtual-environment"></a><span data-ttu-id="4f6d8-163">Controleer of de virtuele omgeving Hallo</span><span class="sxs-lookup"><span data-stu-id="4f6d8-163">Verify hello virtual environment</span></span>
<span data-ttu-id="4f6d8-164">Zorg ervoor dat alles juist is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="4f6d8-165">Hallo-oplossing bouwen door te drukken **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-165">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="4f6d8-166">Wanneer Hallo opbouwbewerking is voltooid, beginnen met het Hallo-website door te drukken **F5**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-166">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="4f6d8-167">Dit start Hallo Flask-ontwikkelaarsserver en uw webbrowser gestart.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-167">This launches hello Flask development server and starts your web browser.</span></span> <span data-ttu-id="4f6d8-168">U ziet Hallo na pagina.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-168">You should see hello following page.</span></span>
   
    ![Hallo lege Python Flask webontwikkelingsproject in een browser](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="4f6d8-170">Stop de foutopsporing Hallo website door te drukken **Shift**+**F5** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-170">Stop debugging hello website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="4f6d8-171">Database-, verzamelings- en documentdefinities maken</span><span class="sxs-lookup"><span data-stu-id="4f6d8-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="4f6d8-172">U kunt nu de stemtoepassing maken door nieuwe bestanden toe te voegen en andere bestanden bij te werken.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="4f6d8-173">Klik in Solution Explorer met de rechtermuisknop op Hallo **zelfstudie** project, klikt u op **toevoegen**, en klik vervolgens op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-173">In Solution Explorer, right-click hello **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="4f6d8-174">Selecteer **lege Python-bestand** en Hallo bestandsnaam **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-174">Select **Empty Python File** and name hello file **forms.py**.</span></span>  
2. <span data-ttu-id="4f6d8-175">Toevoegen Hallo na codebestand toohello forms.py en sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-175">Add hello following code toohello forms.py file, and then save hello file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a><span data-ttu-id="4f6d8-176">Hallo vereist invoer tooviews.py toevoegen</span><span class="sxs-lookup"><span data-stu-id="4f6d8-176">Add hello required imports tooviews.py</span></span>
1. <span data-ttu-id="4f6d8-177">Vouw in Solution Explorer Hallo **zelfstudie** map en open Hallo **views.py** bestand.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-177">In Solution Explorer, expand hello **tutorial** folder, and open hello **views.py** file.</span></span> 
2. <span data-ttu-id="4f6d8-178">Hallo na importeren instructies toohello bovenaan Hallo toevoegen **views.py** bestand en sla vervolgens Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-178">Add hello following import statements toohello top of hello **views.py** file, then save hello file.</span></span> <span data-ttu-id="4f6d8-179">Deze PythonSDK Cosmos-database importeren en Hallo Flask-pakketten.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-179">These import Cosmos DB's PythonSDK and hello Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="4f6d8-180">De database, de verzameling en het document maken</span><span class="sxs-lookup"><span data-stu-id="4f6d8-180">Create database, collection, and document</span></span>
* <span data-ttu-id="4f6d8-181">Nog steeds in **views.py**, Hallo na code toohello einde van bestand Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-181">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="4f6d8-182">Dit zorgt voor het Hallo-database die wordt gebruikt door Hallo formulier maken.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-182">This takes care of creating hello database used by hello form.</span></span> <span data-ttu-id="4f6d8-183">Hallo bestaande code in niet verwijderen **views.py**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-183">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="4f6d8-184">Toe te voegen dit toohello end.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-184">Simply append this toohello end.</span></span>

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="4f6d8-185">De database, de verzameling en het document lezen en het formulier verzenden</span><span class="sxs-lookup"><span data-stu-id="4f6d8-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="4f6d8-186">Nog steeds in **views.py**, Hallo na code toohello einde van bestand Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-186">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="4f6d8-187">Dit zorgt voor het instellen van een formulier Hallo Hallo-database, verzameling en het document te lezen.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-187">This takes care of setting up hello form, reading hello database, collection, and document.</span></span> <span data-ttu-id="4f6d8-188">Hallo bestaande code in niet verwijderen **views.py**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-188">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="4f6d8-189">Toe te voegen dit toohello end.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-189">Simply append this toohello end.</span></span>

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a><span data-ttu-id="4f6d8-190">Hallo HTML-bestanden maken</span><span class="sxs-lookup"><span data-stu-id="4f6d8-190">Create hello HTML files</span></span>
1. <span data-ttu-id="4f6d8-191">Klik in Solution Explorer in Hallo **zelfstudie** map, rechts, klikt u op Hallo **sjablonen** map, klikt u op **toevoegen**, en klik vervolgens op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-191">In Solution Explorer, in hello **tutorial** folder, right click hello **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="4f6d8-192">Selecteer **HTML-pagina**, en klik vervolgens in Hallo naam vak type **create.html**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-192">Select **HTML Page**, and then in hello name box type **create.html**.</span></span> 
3. <span data-ttu-id="4f6d8-193">Herhaal stap 1 en 2 toocreate twee extra HTML-bestanden: results.html en vote.html.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-193">Repeat steps 1 and 2 toocreate two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="4f6d8-194">Hallo code te volgen toevoegen**create.html** in Hallo `<body>` element.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-194">Add hello following code too**create.html** in hello `<body>` element.</span></span> <span data-ttu-id="4f6d8-195">Er wordt een bericht weergegeven dat er een nieuwe database, een nieuwe verzameling en een nieuw document is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="4f6d8-196">Hallo code te volgen toevoegen**results.html** in Hallo `<body`> element.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-196">Add hello following code too**results.html** in hello `<body`> element.</span></span> <span data-ttu-id="4f6d8-197">Hallo-resultaten van Hallo poll wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-197">It displays hello results of hello poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. <span data-ttu-id="4f6d8-198">Hallo code te volgen toevoegen**vote.html** in Hallo `<body`> element.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-198">Add hello following code too**vote.html** in hello `<body`> element.</span></span> <span data-ttu-id="4f6d8-199">Het Hallo poll wordt weergegeven en Hallo stemmen accepteert.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-199">It displays hello poll and accepts hello votes.</span></span> <span data-ttu-id="4f6d8-200">Over het registreren van Hallo stemmen Hallo besturing overgegeven met tooviews.py waar we herkennen Hallo stem cast en Hallo document dienovereenkomstig toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-200">On registering hello votes, hello control is passed over tooviews.py where we will recognize hello vote cast and append hello document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="4f6d8-201">In Hallo **sjablonen** map vervangen Hallo inhoud van **index.html** door Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-201">In hello **templates** folder, replace hello contents of **index.html** with hello following.</span></span> <span data-ttu-id="4f6d8-202">Dit fungeert als Hallo landingspagina voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-202">This serves as hello landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a><span data-ttu-id="4f6d8-203">Een configuratiebestand toevoegen en wijzigen van Hallo \_ \_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="4f6d8-203">Add a configuration file and change hello \_\_init\_\_.py</span></span>
1. <span data-ttu-id="4f6d8-204">Klik in Solution Explorer met de rechtermuisknop op Hallo **zelfstudie** project, klikt u op **toevoegen**, klikt u op **Nieuw Item**, selecteer **lege Python-bestand**, en vervolgens bestand met de Hallo **config.py**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-204">In Solution Explorer, right-click hello **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name hello file **config.py**.</span></span> <span data-ttu-id="4f6d8-205">Dit configuratiebestand is nodig voor de formulieren in Flask.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="4f6d8-206">U kunt deze gebruiken tooprovide ook een geheime sleutel.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-206">You can use it tooprovide a secret key as well.</span></span> <span data-ttu-id="4f6d8-207">Deze sleutel is echter niet nodig voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="4f6d8-208">Voeg de volgende Hallo code tooconfig.py, moet u tooalter Hallo waarden van **DOCUMENTDB\_HOST** en **DOCUMENTDB\_sleutel** in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-208">Add hello following code tooconfig.py, you'll need tooalter hello values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in hello next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="4f6d8-209">In Hallo [Azure-portal](https://portal.azure.com/), navigeer toohello **sleutels** blade door te klikken op **Bladeren**, **Azure Cosmos DB Accounts**, dubbelklikt u op Hallo-naam Hallo toouse account en klik vervolgens op Hallo **sleutels** knop in Hallo **Essentials** gebied.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-209">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click hello name of hello account toouse, and then click hello **Keys** button in hello **Essentials** area.</span></span> <span data-ttu-id="4f6d8-210">In Hallo **sleutels** blade, kopie Hallo **URI** waarde en plak deze in Hallo **config.py** bestand als waarde voor Hallo Hallo **DOCUMENTDB\_HOST**  eigenschap.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-210">In hello **Keys** blade, copy hello **URI** value and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="4f6d8-211">Terug in de Azure-portal, op Hallo Hallo **sleutels** blade kopie Hallo waarde Hallo **primaire sleutel** of Hallo **secundaire sleutel**, en plak deze in Hallo **config.py**  bestand als waarde voor Hallo Hallo **DOCUMENTDB\_sleutel** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-211">Back in hello Azure portal, in hello **Keys** blade, copy hello value of hello **Primary Key** or hello **Secondary Key**, and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="4f6d8-212">In Hallo  **\_ \_init\_\_.py** bestand, Hallo volgt regel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-212">In hello **\_\_init\_\_.py** file, add hello following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="4f6d8-213">Zodat Hallo inhoud van het Hallo-bestand is:</span><span class="sxs-lookup"><span data-stu-id="4f6d8-213">So that hello content of hello file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="4f6d8-214">Na het toevoegen van alle Hallo bestanden er Solution Explorer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="4f6d8-214">After adding all hello files, Solution Explorer should look like this:</span></span>
   
    ![Schermopname van het Hallo Visual Studio Solution Explorer-venster](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="4f6d8-216">Stap 4: de webtoepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4f6d8-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="4f6d8-217">Hallo-oplossing bouwen door te drukken **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-217">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="4f6d8-218">Wanneer Hallo opbouwbewerking is voltooid, beginnen met het Hallo-website door te drukken **F5**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-218">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="4f6d8-219">Hallo hieronder ziet u op het scherm.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-219">You should see hello following on your screen.</span></span>
   
    ![Schermopname van Hallo Python + Azure Cosmos DB Stemtoepassing in een webbrowser](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="4f6d8-221">Klik op **maken/wissen Hallo Voting Database** toogenerate Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-221">Click **Create/Clear hello Voting Database** toogenerate hello database.</span></span>
   
    ![Schermopname van het Hallo pagina maken van Hallo webtoepassing – ontwikkelingsgegevens](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="4f6d8-223">Klik vervolgens op **Vote** (Stemmen) en selecteer uw optie.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-223">Then, click **Vote** and select your option.</span></span>
   
    ![Schermopname van het Hallo-webtoepassing met een vraag waarvoor kan worden gestemd](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="4f6d8-225">Voor elke stem die u uitbrengt, wordt Hallo desbetreffende teller verhoogd.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-225">For every vote you cast, it increments hello appropriate counter.</span></span>
   
    ![Schermopname van het Hallo resultaten van Hallo pagina met stemresultaten](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="4f6d8-227">Stop de foutopsporing voor Hallo project door op Shift + F5 te drukken.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-227">Stop debugging hello project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-hello-web-application-tooazure"></a><span data-ttu-id="4f6d8-228">Stap 5: Hallo web application tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="4f6d8-228">Step 5: Deploy hello web application tooAzure</span></span>
<span data-ttu-id="4f6d8-229">Nu dat u Hallo volledige toepassing correct werkt met Cosmos DB hebt, zal deze tooAzure toodeploy.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-229">Now that you have hello complete application working correctly against Cosmos DB, we're going toodeploy this tooAzure.</span></span>

1. <span data-ttu-id="4f6d8-230">Klik met de rechtermuisknop Hallo-project in Solution Explorer (Zorg ervoor dat u niet bent nog steeds lokaal wordt uitgevoerd) en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-230">Right-click hello project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Schermopname van Hallo geselecteerde zelfstudie in Solution Explorer met de optie publiceren Hallo gemarkeerd](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="4f6d8-232">In Hallo **publiceren** dialoogvenster, **Microsoft Azure App Service**, selecteer **nieuw**, en klik vervolgens op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-232">In hello **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Schermopname van Hallo webpublicatie venster met Microsoft Azure App Service is gemarkeerd](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="4f6d8-234">In Hallo **Create App Service** dialoogvenster Hallo- naam voor uw web-app samen met uw **abonnement**, **resourcegroep**, en **App Service-Plan** , klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-234">In hello **Create App Service** dialog box, enter hello name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Schermopname van het Hallo Microsoft Azure Web Apps venster venster](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="4f6d8-236">Binnen een paar seconden zal Visual Studio publicatie van uw app service voltooien en een browser starten waarin u kunt zien uw werk in Azure wordt uitgevoerd!</span><span class="sxs-lookup"><span data-stu-id="4f6d8-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Schermopname van het Hallo Microsoft Azure Web Apps venster venster](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="4f6d8-238">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="4f6d8-238">Troubleshooting</span></span>
<span data-ttu-id="4f6d8-239">Als dit Hallo eerste Python-app u hebt uitgevoerd op uw computer, controleert u of Hallo de volgende mappen (of gelijkwaardige installatielocaties voor Hallo) zijn opgenomen in de variabele PATH:</span><span class="sxs-lookup"><span data-stu-id="4f6d8-239">If this is hello first Python app you've run on your computer, ensure that hello following folders (or hello equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="4f6d8-240">Als u een foutbericht weergegeven op de stempagina en u met de naam uw project iets anders dan **zelfstudie**, zorg ervoor dat  **\_ \_init\_\_.py** verwijzingen Hallo juiste projectnaam in Hallo regel: `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references hello correct project name in hello line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f6d8-241">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4f6d8-241">Next steps</span></span>
<span data-ttu-id="4f6d8-242">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-242">Congratulations!</span></span> <span data-ttu-id="4f6d8-243">U hebt zojuist uw eerste Python-webtoepassing met behulp van de Cosmos-DB voltooid en tooAzure gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-243">You have just completed your first Python web application using Cosmos DB and published it tooAzure.</span></span>

<span data-ttu-id="4f6d8-244">Dit onderwerp wordt regelmatig bijgewerkt en verbeterd op basis van uw feedback.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="4f6d8-245">Eenmaal u Hallo-zelfstudie hebt voltooid met Neem Hallo stemknoppen Hallo boven en onder aan deze pagina, en ervoor tooinclude uw feedback op welke verbeteringen toosee aangebracht gewenste.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-245">Once you've completed hello tutorial, please using hello voting buttons at hello top and bottom of this page, and be sure tooinclude your feedback on what improvements you want toosee made.</span></span> <span data-ttu-id="4f6d8-246">Als u graag toocontact u rechtstreeks kunt u gratis tooinclude je e-mailadres in uw opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="4f6d8-246">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="4f6d8-247">tooadd aanvullende functionaliteit tooyour webtoepassing, bekijk Hallo beschikbare API's in Hallo [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-247">tooadd additional functionality tooyour web application, review hello APIs available in hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="4f6d8-248">Zie voor meer informatie over Azure, Visual Studio en Python Hallo [Python Developer Center](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-248">For more information about Azure, Visual Studio, and Python, see hello [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="4f6d8-249">Zie voor aanvullende zelfstudies over Python Flask [hello Flask Mega-Tutorial, deel I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span><span class="sxs-lookup"><span data-stu-id="4f6d8-249">For additional Python Flask tutorials, see [hello Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com

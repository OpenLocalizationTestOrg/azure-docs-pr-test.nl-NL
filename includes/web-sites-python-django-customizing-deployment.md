<span data-ttu-id="f1ee1-101">Azure bepaalt dat uw toepassing Python gebruikt **als beide volgende voorwaarden waar zijn**:</span><span class="sxs-lookup"><span data-stu-id="f1ee1-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="f1ee1-102">bestand requirements.txt in de hoofdmap</span><span class="sxs-lookup"><span data-stu-id="f1ee1-102">requirements.txt file in the root folder</span></span>
* <span data-ttu-id="f1ee1-103">elk bestand .py in de hoofdmap OF een runtime.txt die Python specificeert</span><span class="sxs-lookup"><span data-stu-id="f1ee1-103">any .py file in the root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="f1ee1-104">Wanneer dit het geval is, wordt een implementatiescript gebruikt dat specifiek is voor Python en waarmee de standaard synchronisatie van bestanden wordt uitgevoerd, evenals extra Python-bewerkingen zoals:</span><span class="sxs-lookup"><span data-stu-id="f1ee1-104">When that's the case, it will use a Python specific deployment script, which performs the standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="f1ee1-105">Automatisch beheer van virtuele omgeving</span><span class="sxs-lookup"><span data-stu-id="f1ee1-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="f1ee1-106">Installatie van pakketten die zijn vermeld in requirements.txt met behulp van pip</span><span class="sxs-lookup"><span data-stu-id="f1ee1-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="f1ee1-107">Maken van de juiste web.config op basis van de geselecteerde Python-versie</span><span class="sxs-lookup"><span data-stu-id="f1ee1-107">Creation of the appropriate web.config based on the selected Python version.</span></span>
* <span data-ttu-id="f1ee1-108">Verzamelen van statische bestanden voor Django-toepassingen</span><span class="sxs-lookup"><span data-stu-id="f1ee1-108">Collect static files for Django applications</span></span>

<span data-ttu-id="f1ee1-109">U kunt bepaalde aspecten van de standaard implementatiestappen beheren zonder dat u het script hoeft aan te passen.</span><span class="sxs-lookup"><span data-stu-id="f1ee1-109">You can control certain aspects of the default deployment steps without having to customize the script.</span></span>

<span data-ttu-id="f1ee1-110">Als u alle stappen die specifiek zijn voor de implementatie van Python wilt overslaan, kunt u dit lege bestand maken:</span><span class="sxs-lookup"><span data-stu-id="f1ee1-110">If you want to skip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="f1ee1-111">Als u het verzamelen van statische bestanden voor uw Django-toepassing wilt overslaan:</span><span class="sxs-lookup"><span data-stu-id="f1ee1-111">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango 

<span data-ttu-id="f1ee1-112">Voor meer controle over de implementatie kunt u het standaard implementatiescript overschrijven door de volgende bestanden te maken:</span><span class="sxs-lookup"><span data-stu-id="f1ee1-112">For more control over deployment, you can override the default deployment script by creating the following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="f1ee1-113">U kunt de [Azure-opdrachtregelinterface] [ Azure command-line interface] om de bestanden te maken.</span><span class="sxs-lookup"><span data-stu-id="f1ee1-113">You can use the [Azure command-line interface][Azure command-line interface] to create the files.</span></span>  <span data-ttu-id="f1ee1-114">Gebruik deze opdracht uit vanuit de projectmap:</span><span class="sxs-lookup"><span data-stu-id="f1ee1-114">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="f1ee1-115">Als deze bestanden niet bestaan, maakt Azure een tijdelijk implementatiescript en voert dit script uit.</span><span class="sxs-lookup"><span data-stu-id="f1ee1-115">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="f1ee1-116">Het is identiek aan het script dat u met de bovenstaande opdracht maakt.</span><span class="sxs-lookup"><span data-stu-id="f1ee1-116">It is identical to the one you create with the command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/

<span data-ttu-id="0cc7c-101">Azure bepaalt dat uw toepassing Python gebruikt **als beide volgende voorwaarden waar zijn**:</span><span class="sxs-lookup"><span data-stu-id="0cc7c-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="0cc7c-102">bestand Requirements.txt in de hoofdmap Hallo</span><span class="sxs-lookup"><span data-stu-id="0cc7c-102">requirements.txt file in hello root folder</span></span>
* <span data-ttu-id="0cc7c-103">elk bestand .py in de hoofdmap hello of een runtime.txt die python specificeert</span><span class="sxs-lookup"><span data-stu-id="0cc7c-103">any .py file in hello root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="0cc7c-104">Wanneer die Hallo geval is, wordt een specifieke implementatie pythonscript, waarmee Hallo standaard synchronisatie van bestanden, evenals extra Python-bewerkingen zoals gebruikt:</span><span class="sxs-lookup"><span data-stu-id="0cc7c-104">When that's hello case, it will use a Python specific deployment script, which performs hello standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="0cc7c-105">Automatisch beheer van virtuele omgeving</span><span class="sxs-lookup"><span data-stu-id="0cc7c-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="0cc7c-106">Installatie van pakketten die zijn vermeld in requirements.txt met behulp van pip</span><span class="sxs-lookup"><span data-stu-id="0cc7c-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="0cc7c-107">Maken van de juiste web.config Hallo op basis van Hallo geselecteerde Python-versie.</span><span class="sxs-lookup"><span data-stu-id="0cc7c-107">Creation of hello appropriate web.config based on hello selected Python version.</span></span>
* <span data-ttu-id="0cc7c-108">Verzamelen van statische bestanden voor Django-toepassingen</span><span class="sxs-lookup"><span data-stu-id="0cc7c-108">Collect static files for Django applications</span></span>

<span data-ttu-id="0cc7c-109">U kunt bepaalde aspecten van Hallo standaard implementatiestappen beheren zonder toocustomize Hallo script.</span><span class="sxs-lookup"><span data-stu-id="0cc7c-109">You can control certain aspects of hello default deployment steps without having toocustomize hello script.</span></span>

<span data-ttu-id="0cc7c-110">Als u wilt dat tooskip alle stappen voor Python-specifieke implementatie, kunt u dit lege bestand maken:</span><span class="sxs-lookup"><span data-stu-id="0cc7c-110">If you want tooskip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="0cc7c-111">Als u wilt dat tooskip verzamelen van statische bestanden voor uw Django-toepassing:</span><span class="sxs-lookup"><span data-stu-id="0cc7c-111">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango 

<span data-ttu-id="0cc7c-112">Voor meer controle over de implementatie kunt u Hallo standaard implementatiescript overschrijven door het maken van de volgende bestanden Hallo:</span><span class="sxs-lookup"><span data-stu-id="0cc7c-112">For more control over deployment, you can override hello default deployment script by creating hello following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="0cc7c-113">U kunt Hallo [Azure-opdrachtregelinterface] [ Azure command-line interface] toocreate Hallo-bestanden.</span><span class="sxs-lookup"><span data-stu-id="0cc7c-113">You can use hello [Azure command-line interface][Azure command-line interface] toocreate hello files.</span></span>  <span data-ttu-id="0cc7c-114">Gebruik deze opdracht uit vanuit de projectmap:</span><span class="sxs-lookup"><span data-stu-id="0cc7c-114">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="0cc7c-115">Als deze bestanden niet bestaan, maakt Azure een tijdelijk implementatiescript en voert dit script uit.</span><span class="sxs-lookup"><span data-stu-id="0cc7c-115">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="0cc7c-116">Het is identiek toohello één u maken met de bovenstaande Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="0cc7c-116">It is identical toohello one you create with hello command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/

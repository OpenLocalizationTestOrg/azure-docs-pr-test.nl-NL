<span data-ttu-id="ed420-101">Sommige pakketten kunnen niet worden geïnstalleerd met pip wanneer ze worden uitgevoerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="ed420-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="ed420-102">Dit kan eenvoudig komen dat Hallo-pakket is niet beschikbaar op Hallo Python Package Index.</span><span class="sxs-lookup"><span data-stu-id="ed420-102">It may simply be that hello package is not available on hello Python Package Index.</span></span>  <span data-ttu-id="ed420-103">Kan het zijn dat een compiler vereist is (een compiler is niet beschikbaar op Hallo machine uitgevoerd Hallo web-app in Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="ed420-103">It could be that a compiler is required (a compiler is not available on hello machine running hello web app in Azure App Service).</span></span>

<span data-ttu-id="ed420-104">In deze sectie zullen we manieren toodeal bij dit probleem.</span><span class="sxs-lookup"><span data-stu-id="ed420-104">In this section, we'll look at ways toodeal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="ed420-105">Wheels aanvragen</span><span class="sxs-lookup"><span data-stu-id="ed420-105">Request wheels</span></span>
<span data-ttu-id="ed420-106">Als het Hallo-pakketinstallatie een compiler vereist, moet u Neem contact op met Hallo pakket eigenaar toorequest wheels beschikbaar gesteld voor Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="ed420-106">If hello package installation requires a compiler, you should try contacting hello package owner toorequest that wheels be made available for hello package.</span></span>

<span data-ttu-id="ed420-107">Met de recente beschikbaarheid Hallo van [Microsoft Visual C++ Compiler voor Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], is nu eenvoudiger toobuild pakketten met systeemeigen code voor Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="ed420-107">With hello recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier toobuild packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="ed420-108">Wheels bouwen (vereist Windows)</span><span class="sxs-lookup"><span data-stu-id="ed420-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="ed420-109">Opmerking: Wanneer u deze optie gebruikt, zorg ervoor dat toocompile Hallo pakket met behulp van een Python-omgeving die overeenkomt met de Hallo platform of architectuur of versie die wordt gebruikt op Hallo web-app in Azure App Service (Windows/32-bit/2.7 of 3.4).</span><span class="sxs-lookup"><span data-stu-id="ed420-109">Note: When using this option, make sure toocompile hello package using a Python environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="ed420-110">Hallo-pakket wordt niet geïnstalleerd omdat het een compiler vereist, kunt u Hallo compiler installeren op uw lokale machine en een wheel bouwen voor Hallo-pakket dat u vervolgens kunt in uw opslagplaats opnemen.</span><span class="sxs-lookup"><span data-stu-id="ed420-110">If hello package doesn't install because it requires a compiler, you can install hello compiler on your local machine and build a wheel for hello package, which you will then include in your repository.</span></span>

<span data-ttu-id="ed420-111">Gebruikers van Mac/Linux: Als u geen toegang tot tooa Windows-computer, Zie [maken van een virtuele Machine met Windows] [ Create a Virtual Machine Running Windows] voor het toocreate een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="ed420-111">Mac/Linux Users: If you don't have access tooa Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how toocreate a VM on Azure.</span></span>  <span data-ttu-id="ed420-112">U kunt toobuild Hallo wheels worden gebruikt, deze opslagplaats toohello toevoegen en Hallo VM desgewenst verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ed420-112">You can use it toobuild hello wheels, add them toohello repository, and discard hello VM if you like.</span></span> 

<span data-ttu-id="ed420-113">U kunt installeren voor Python 2.7 [Microsoft Visual C++ Compiler voor Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span><span class="sxs-lookup"><span data-stu-id="ed420-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="ed420-114">U kunt installeren voor Python 3.4 [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span><span class="sxs-lookup"><span data-stu-id="ed420-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="ed420-115">wheels toobuild, hebt u Hallo wheel-pakket nodig:</span><span class="sxs-lookup"><span data-stu-id="ed420-115">toobuild wheels, you'll need hello wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="ed420-116">U `pip wheel` toocompile een afhankelijkheid:</span><span class="sxs-lookup"><span data-stu-id="ed420-116">You'll use `pip wheel` toocompile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="ed420-117">Hiermee maakt u een .whl-bestand in de map \wheelhouse Hallo.</span><span class="sxs-lookup"><span data-stu-id="ed420-117">This creates a .whl file in hello \wheelhouse folder.</span></span>  <span data-ttu-id="ed420-118">De map \wheelhouse hello en wheel-bestanden tooyour opslagplaats toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ed420-118">Add hello \wheelhouse folder and wheel files tooyour repository.</span></span>

<span data-ttu-id="ed420-119">Bewerken van uw requirements.txt tooadd hello `--find-links` optie Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="ed420-119">Edit your requirements.txt tooadd hello `--find-links` option at hello top.</span></span> <span data-ttu-id="ed420-120">Hiermee wordt de pip toolook schrijfopdrachten naar een exacte overeenkomst in de lokale map Hallo voor voortdurende toohello python package index.</span><span class="sxs-lookup"><span data-stu-id="ed420-120">This tells pip toolook for an exact match in hello local folder before going toohello python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="ed420-121">Als u wilt dat alle afhankelijkheden in Hallo \wheelhouse map en geen gebruik Hallo python-pakket index helemaal tooinclude, kunt u pip tooignore Hallo package index forceren door toe te voegen `--no-index` toohello boven Requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="ed420-121">If you want tooinclude all your dependencies in hello \wheelhouse folder and not use hello python package index at all, you can force pip tooignore hello package index by adding `--no-index` toohello top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="ed420-122">Installatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="ed420-122">Customize installation</span></span>
<span data-ttu-id="ed420-123">U kunt aanpassen Hallo implementatie script tooinstall een pakket in Hallo virtuele omgeving met een alternatief installatieprogramma zoals easy\_installeren.</span><span class="sxs-lookup"><span data-stu-id="ed420-123">You can customize hello deployment script tooinstall a package in hello virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="ed420-124">Zie deploy.cmd voor een voorbeeld met opmerkingen.  Zorg ervoor dat dergelijke pakketten zijn niet opgenomen in requirements.txt tooprevent pip ze installeert.</span><span class="sxs-lookup"><span data-stu-id="ed420-124">See deploy.cmd for an example that is commented out.  Make sure that such packages aren't listed in requirements.txt, tooprevent pip from installing them.</span></span>

<span data-ttu-id="ed420-125">Dit script toohello implementatie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="ed420-125">Add this toohello deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="ed420-126">Hebt u mogelijk ook kunnen eenvoudig toouse\_tooinstall installeren vanaf een exe-installatieprogramma (sommige zijn zip-compatibel, dus eenvoudige\_installatie ondersteunt).</span><span class="sxs-lookup"><span data-stu-id="ed420-126">You may also be able toouse easy\_install tooinstall from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="ed420-127">Voeg Hallo installatieprogramma tooyour opslagplaats toe en roep easy\_installeren met de Hallo pad toohello uitvoerbare doorgeven.</span><span class="sxs-lookup"><span data-stu-id="ed420-127">Add hello installer tooyour repository, and invoke easy\_install by passing hello path toohello executable.</span></span>

<span data-ttu-id="ed420-128">Dit script toohello implementatie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="ed420-128">Add this toohello deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a><span data-ttu-id="ed420-129">Hallo virtuele omgeving opnemen in Hallo-opslagplaats (vereist Windows)</span><span class="sxs-lookup"><span data-stu-id="ed420-129">Include hello virtual environment in hello repository (requires Windows)</span></span>
<span data-ttu-id="ed420-130">Opmerking: Wanneer u deze optie gebruikt, zorg ervoor dat toouse een virtuele omgeving die overeenkomt met de Hallo platform of architectuur of versie die wordt gebruikt op Hallo web-app in Azure App Service (Windows/32-bit/2.7 of 3.4).</span><span class="sxs-lookup"><span data-stu-id="ed420-130">Note: When using this option, make sure toouse a virtual environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="ed420-131">Als u Hallo virtuele omgeving in de opslagplaats hello opneemt, kunt u voorkomen dat het implementatiescript Hallo virtuele omgeving op Azure beheeractiviteiten doen door een leeg bestand te maken:</span><span class="sxs-lookup"><span data-stu-id="ed420-131">If you include hello virtual environment in hello repository, you can prevent hello deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="ed420-132">Het is raadzaam dat u Hallo bestaande virtuele omgeving op Hallo app tooprevent er bestanden overblijven uit verwijdert wanneer Hallo virtuele omgeving automatisch werd beheerd.</span><span class="sxs-lookup"><span data-stu-id="ed420-132">We recommend that you delete hello existing virtual environment on hello app, tooprevent leftover files from when hello virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949

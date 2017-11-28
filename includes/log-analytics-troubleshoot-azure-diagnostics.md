### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="77f57-101">Problemen oplossen met Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="77f57-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="77f57-102">Als u het volgende foutbericht ontvangt, is de resourceprovider Microsoft.insights niet geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="77f57-102">If you receive the following error message, the Microsoft.insights resource provider is not registered:</span></span>

`Failed to update diagnostics for 'resource'. {"code":"Forbidden","message":"Please register the subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="77f57-103">Voer de volgende stappen in Azure Portal uit om de resourceprovider te registreren:</span><span class="sxs-lookup"><span data-stu-id="77f57-103">To register the resource provider, perform the following steps in the Azure portal:</span></span>

1.  <span data-ttu-id="77f57-104">Klik in het navigatiedeelvenster aan de linkerkant op *Abonnementen*</span><span class="sxs-lookup"><span data-stu-id="77f57-104">In the navigation pane on the left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="77f57-105">Selecteer het abonnement dat wordt vermeld in het foutbericht</span><span class="sxs-lookup"><span data-stu-id="77f57-105">Select the subscription identified in the error message</span></span>
3.  <span data-ttu-id="77f57-106">Klik op *Resourceproviders*</span><span class="sxs-lookup"><span data-stu-id="77f57-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="77f57-107">Ga naar de *Microsoft.insights*-provider</span><span class="sxs-lookup"><span data-stu-id="77f57-107">Find the *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="77f57-108">Klik op de koppeling *Registreren*</span><span class="sxs-lookup"><span data-stu-id="77f57-108">Click the *Register* link</span></span>

![Registreer de resourceprovider Microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="77f57-110">Nadat de *Microsoft.insights* resourceprovider is geregistreerd, configureert u Diagnostics opnieuw.</span><span class="sxs-lookup"><span data-stu-id="77f57-110">Once the *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="77f57-111">Als u het volgende foutbericht ontvangt in PowerShell moet u werk uw versie van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="77f57-111">In PowerShell, if you receive the following error message, you need to update your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="77f57-112">Werk uw versie van PowerShell naar de November 2016 (v2.3.0) of hoger, vrijgeven van de instructies in de [aan de slag met Azure PowerShell-cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) artikel.</span><span class="sxs-lookup"><span data-stu-id="77f57-112">Update your version of PowerShell to the November 2016 (v2.3.0), or later, release using the instructions in the [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>

### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="a0876-101">Problemen oplossen met Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="a0876-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="a0876-102">Als u Hallo volgende foutbericht wordt weergegeven ontvangt, is niet Hallo Microsoft.insights-resourceprovider geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="a0876-102">If you receive hello following error message, hello Microsoft.insights resource provider is not registered:</span></span>

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="a0876-103">tooregister hello resourceprovider uitvoeren Hallo stappen te volgen in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="a0876-103">tooregister hello resource provider, perform hello following steps in hello Azure portal:</span></span>

1.  <span data-ttu-id="a0876-104">Klik in het navigatievenster aan de linkerkant Hallo Hallo *abonnementen*</span><span class="sxs-lookup"><span data-stu-id="a0876-104">In hello navigation pane on hello left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="a0876-105">Selecteer geïdentificeerd in het foutbericht Hallo Hallo-abonnement</span><span class="sxs-lookup"><span data-stu-id="a0876-105">Select hello subscription identified in hello error message</span></span>
3.  <span data-ttu-id="a0876-106">Klik op *Resourceproviders*</span><span class="sxs-lookup"><span data-stu-id="a0876-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="a0876-107">Hallo zoeken *Microsoft.insights* provider</span><span class="sxs-lookup"><span data-stu-id="a0876-107">Find hello *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="a0876-108">Klik op Hallo *registreren* koppeling</span><span class="sxs-lookup"><span data-stu-id="a0876-108">Click hello *Register* link</span></span>

![Registreer de resourceprovider Microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="a0876-110">Eenmaal Hallo *Microsoft.insights* resourceprovider is geregistreerd, opnieuw proberen van configuratie van diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a0876-110">Once hello *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="a0876-111">In PowerShell, als het foutbericht Hallo volgende foutbericht wordt weergegeven, moet u tooupdate uw versie van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a0876-111">In PowerShell, if you receive hello following error message, you need tooupdate your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="a0876-112">Werk uw versie van PowerShell toohello November 2016 (v2.3.0) of hoger, vrijgeven met Hallo-instructies in Hallo [aan de slag met Azure PowerShell-cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) artikel.</span><span class="sxs-lookup"><span data-stu-id="a0876-112">Update your version of PowerShell toohello November 2016 (v2.3.0), or later, release using hello instructions in hello [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>

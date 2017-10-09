### <a name="troubleshoot-azure-diagnostics"></a>Problemen oplossen met Azure Diagnostics

Als u Hallo volgende foutbericht wordt weergegeven ontvangt, is niet Hallo Microsoft.insights-resourceprovider geregistreerd:

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

tooregister hello resourceprovider uitvoeren Hallo stappen te volgen in hello Azure-portal:

1.  Klik in het navigatievenster aan de linkerkant Hallo Hallo *abonnementen*
2.  Selecteer geïdentificeerd in het foutbericht Hallo Hallo-abonnement
3.  Klik op *Resourceproviders*
4.  Hallo zoeken *Microsoft.insights* provider
5.  Klik op Hallo *registreren* koppeling

![Registreer de resourceprovider Microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

Eenmaal Hallo *Microsoft.insights* resourceprovider is geregistreerd, opnieuw proberen van configuratie van diagnostische gegevens.


In PowerShell, als het foutbericht Hallo volgende foutbericht wordt weergegeven, moet u tooupdate uw versie van PowerShell:

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

Werk uw versie van PowerShell toohello November 2016 (v2.3.0) of hoger, vrijgeven met Hallo-instructies in Hallo [aan de slag met Azure PowerShell-cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) artikel.

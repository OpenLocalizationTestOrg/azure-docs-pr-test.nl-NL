#### <a name="toostop-and-start-a-virtual-device"></a>toostop en start een virtueel apparaat
een virtueel apparaat toostop Klik op de naam en klik vervolgens op **afsluiten**. Terwijl het virtuele apparaat hello wordt afgesloten, wordt de status ervan is **stoppen**. Nadat het virtuele apparaat Hallo is gestopt, wordt de status ervan is **gestopt**.

Gebruik Hallo cmdlets toostop te volgen en een virtueel apparaat starten.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a>een virtueel apparaat toorestart
Wanneer een virtueel apparaat wordt uitgevoerd en u wilt toorestart, klik op de naam en klik vervolgens op **opnieuw**. Terwijl Hallo virtueel apparaat opnieuw wordt opgestart, wordt de status ervan is **wordt opnieuw gestart**. Wanneer het virtuele apparaat Hallo gereed voor u toouse is, de status ervan is **met**.

Gebruik Hallo cmdlet toorestart een virtueel apparaat te volgen.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`


#### <a name="toostop-and-start-a-cloud-appliance"></a>toostop en start een cloud-apparaat

1. toostop een cloud-apparaat gaat toohello VM voor uw toestel cloud.
    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)

2. Hallo opdrachtbalk en klik op **stoppen**.

    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. Klik op **Ja** als u om bevestiging wordt gevraagd.

    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. Wanneer u een virtuele machine stopt, wordt de toewijzing ervan opgeheven. Hoewel Hallo cloud toestel wordt gestopt, is het de status ervan **Deallocating**. Nadat de Hallo cloud toestel is gestopt, wordt de status ervan is **gestopt (toewijzing opgeheven)**.

    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. Wanneer een virtuele machine is gestopt, klikt u op **Start** (knop beschikbaar) toostart Hallo VM. Nadat het Hallo cloud toestel is gestart, is het de status ervan **gestart**.

    ![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

Gebruik Hallo cmdlets toostop te volgen en starten van een cloud-apparaat.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a>toorestart een cloud-apparaat

toorestart een cloud-apparaat gaat toohello VM voor uw toestel cloud. Hallo opdrachtbalk en klik op **opnieuw**. Wanneer u wordt gevraagd, bevestig Hallo opnieuw opstarten. Wanneer Hallo cloud toestel gereed voor u toouse is, de status ervan is **met**.

![StorSimple-cloudapparaat - virtuele machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

Hallo volgende cmdlet toorestart een cloud-apparaat gebruiken.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`


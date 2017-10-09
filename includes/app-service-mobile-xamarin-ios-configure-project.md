#### <a name="configure-hello-ios-project-in-xamarin-studio"></a>Hallo iOS-project in Xamarin Studio configureren
1. Open in Xamarin.Studio, **Info.plist**, en update Hallo **bundel-id** Hello bundel-ID die u eerder hebt gemaakt met uw nieuwe app-ID.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. Schuif naar beneden te**Achtergrondmodi**. Selecteer Hallo **Enable Background Modes** vak en Hallo **Remote notifications** vak.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. Dubbelklik op het project in Hallo oplossing Configuratiescherm tooopen **Projectopties**.
4. Onder **bouwen**, kies **iOS bundel ondertekening**, en selecteer Hallo bijbehorende identiteit en inrichtingsprofiel u net hebt ingesteld voor dit project.

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   Dit zorgt ervoor dat project Hallo Hallo nieuwe profiel wordt gebruikt voor ondertekening van programmacode. Hallo officiële Xamarin apparaten inrichten documentatie, Zie [Xamarin apparaten inrichten].

#### <a name="configure-hello-ios-project-in-visual-studio"></a>Hallo iOS-project in Visual Studio configureren
1. Met de rechtermuisknop op het Hallo-project in Visual Studio en klik vervolgens op **eigenschappen**.
2. Klik in de pagina eigenschappen van Hallo op Hallo **iOS-toepassing** tabblad en update Hallo **id** Hallo-id die u eerder hebt gemaakt.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. In Hallo **iOS bundel ondertekening** tabblad Selecteer Hallo bijbehorende identiteit en de inrichting profiel u zojuist hebt ingesteld om voor dit project.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    Dit zorgt ervoor dat project Hallo Hallo nieuwe profiel wordt gebruikt voor ondertekening van programmacode. Hallo officiële Xamarin apparaten inrichten documentatie, Zie [Xamarin apparaten inrichten].
4. Dubbelklik op Info.plist tooopen en schakelt u vervolgens **RemoteNotifications** onder **Achtergrondmodi**.

[Xamarin apparaten inrichten]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/

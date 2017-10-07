---
title: aaaHow toouse Blob Storage uit het Xamarin | Microsoft Docs
description: Hello Azure Storage-clientbibliotheek voor Xamarin kan ontwikkelaars toocreate iOS, Android en Windows Store-apps met hun eigen gebruikersinterface. Deze zelfstudie laat zien hoe toouse Xamarin toocreate een toepassing die gebruikmaakt van Azure Blob-opslag.
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 751f66d1d2392c8bcf6e5f8d1b185af73582fab3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a>Hoe toouse Xamarin Blob-opslag
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a>Overzicht
Xamarin kunnen ontwikkelaars toouse een gedeelde C# codebase toocreate iOS, Android en Windows Store-apps met hun eigen gebruikersinterface. Deze zelfstudie leert u hoe toouse Azure Blob storage met een Xamarin-toepassing. Als u meer informatie over Azure Storage toolearn wilt vooraleer Hallo code, Zie [tooMicrosoft inleiding Azure Storage](storage-introduction.md).

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a>Maak een nieuwe Xamarin-toepassing
Voor deze zelfstudie maakt er een app die gericht is op Android, iOS en Windows. Deze app wordt gewoon een container maken en een blob uploadt naar deze container. We wilt Visual Studio gebruiken op Windows, maar Hallo dezelfde geleerde lessen kunnen worden toegepast bij het maken van een app met Xamarin Studio op Mac OS.

Volg deze stappen toocreate uw toepassing:

1. Als u dat nog niet gedaan hebt, downloaden en installeren [Xamarin voor Visual Studio](https://www.xamarin.com/download).
2. Open Visual Studio en maakt een lege App (systeemeigen draagbare): **bestand > Nieuw > Project > platformoverschrijdende > lege App(Native Portable)**.
3. Met de rechtermuisknop op uw oplossing in Solution Explorer-venster Hallo en selecteer **NuGet-pakketten beheren voor oplossing**. Zoeken naar **WindowsAzure.Storage** en installeer Hallo nieuwste stabiele versie tooall projecten in uw oplossing.
4. Ontwikkel en voer uw project.

U hebt nu een toepassing waarmee u tooclick een knop waarmee een item wordt verhoogd.

## <a name="create-container-and-upload-blob"></a>Container maken en uploaden van blob
Vervolgens onder uw `(Portable)` project, voegt u code te`MyClass.cs`. Deze code maakt een container en een blob uploadt naar deze container. `MyClass.cs`moet eruitzien als Hallo volgende:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create hello blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference tooa previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create hello container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference tooa blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create hello "myblob" blob with hello text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

Zorg ervoor dat tooreplace 'your_account_name_here' en 'your_account_key_here' werkelijke accountnaam en accountsleutel van uw. 

Uw iOS-, Android en Windows Phone-projecten alle verwijzingen tooyour draagbare project hebben-wat betekent dat u alle gedeelde code kunt schrijven in een plaats en deze gebruiken voor alle projecten. Nu kunt u de volgende regel code tooeach project toostart profiteert Hallo toevoegen:`MyClass.performBlobOperation()`

### <a name="xamarinappdroid--mainactivitycs"></a>XamarinApp.Droid > MainActivity.cs

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a>XamarinApp.iOS > ViewController.cs

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading hello view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a>XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// hello Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated toowithin a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about toobe displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used tooconfigure hello page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about toobe displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used tooconfigure hello page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling hello hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using hello NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren
U kunt deze toepassing nu uitvoeren in een Android- of Windows Phone-emulator. U kunt deze toepassing ook uitvoeren in een iOS-emulator, maar hiervoor moet een Mac. Voor specifieke instructies over hoe toodo, documentatie te lezen Hallo voor [verbinding maken met Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)

Als u uw app hebt uitgevoerd, Hallo-container gemaakt wordt `mycontainer` in uw opslagaccount. Hallo-blob bevatten moeten `myblob`, die de tekst hello, heeft `Hello, world!`. U kunt dit controleren met behulp van Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe een toepassing platformoverschrijdende in Xamarin toocreate die gebruikmaakt van Azure Storage, specifiek gericht op een scenario in Blob Storage. Echter, u kunt doen veel meer met niet alleen de Blob-opslag, maar ook met tabel-, bestands- en Queue Storage. Kijk eens Hallo artikelen toolearn meer te volgen:

* [Aan de slag met Azure Blob Storage met .NET](storage-dotnet-how-to-use-blobs.md)
* [Aan de slag met Azure Table Storage met .NET](storage-dotnet-how-to-use-tables.md)
* [Aan de slag met Azure Queue Storage met .NET](storage-dotnet-how-to-use-queues.md)
* [Aan de slag met Azure File Storage in Windows](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]


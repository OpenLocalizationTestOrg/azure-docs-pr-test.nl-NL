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
# <a name="how-toouse-blob-storage-from-xamarin"></a><span data-ttu-id="ff8b0-104">Hoe toouse Xamarin Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="ff8b0-104">How toouse Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="ff8b0-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ff8b0-105">Overview</span></span>
<span data-ttu-id="ff8b0-106">Xamarin kunnen ontwikkelaars toouse een gedeelde C# codebase toocreate iOS, Android en Windows Store-apps met hun eigen gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-106">Xamarin enables developers toouse a shared C# codebase toocreate iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="ff8b0-107">Deze zelfstudie leert u hoe toouse Azure Blob storage met een Xamarin-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-107">This tutorial shows you how toouse Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="ff8b0-108">Als u meer informatie over Azure Storage toolearn wilt vooraleer Hallo code, Zie [tooMicrosoft inleiding Azure Storage](storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ff8b0-108">If you'd like toolearn more about Azure Storage, before diving into hello code, see [Introduction tooMicrosoft Azure Storage](storage-introduction.md).</span></span>

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="ff8b0-109">Maak een nieuwe Xamarin-toepassing</span><span class="sxs-lookup"><span data-stu-id="ff8b0-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="ff8b0-110">Voor deze zelfstudie maakt er een app die gericht is op Android, iOS en Windows.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="ff8b0-111">Deze app wordt gewoon een container maken en een blob uploadt naar deze container.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="ff8b0-112">We wilt Visual Studio gebruiken op Windows, maar Hallo dezelfde geleerde lessen kunnen worden toegepast bij het maken van een app met Xamarin Studio op Mac OS.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-112">We'll be using Visual Studio on Windows, but hello same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="ff8b0-113">Volg deze stappen toocreate uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="ff8b0-113">Follow these steps toocreate your application:</span></span>

1. <span data-ttu-id="ff8b0-114">Als u dat nog niet gedaan hebt, downloaden en installeren [Xamarin voor Visual Studio](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="ff8b0-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="ff8b0-115">Open Visual Studio en maakt een lege App (systeemeigen draagbare): **bestand > Nieuw > Project > platformoverschrijdende > lege App(Native Portable)**.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="ff8b0-116">Met de rechtermuisknop op uw oplossing in Solution Explorer-venster Hallo en selecteer **NuGet-pakketten beheren voor oplossing**.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-116">Right-click your solution in hello Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="ff8b0-117">Zoeken naar **WindowsAzure.Storage** en installeer Hallo nieuwste stabiele versie tooall projecten in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-117">Search for **WindowsAzure.Storage** and install hello latest stable version tooall projects in your solution.</span></span>
4. <span data-ttu-id="ff8b0-118">Ontwikkel en voer uw project.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-118">Build and run your project.</span></span>

<span data-ttu-id="ff8b0-119">U hebt nu een toepassing waarmee u tooclick een knop waarmee een item wordt verhoogd.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-119">You should now have an application that allows you tooclick a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="ff8b0-120">Container maken en uploaden van blob</span><span class="sxs-lookup"><span data-stu-id="ff8b0-120">Create container and upload blob</span></span>
<span data-ttu-id="ff8b0-121">Vervolgens onder uw `(Portable)` project, voegt u code te`MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-121">Next, under your `(Portable)` project, you'll add some code too`MyClass.cs`.</span></span> <span data-ttu-id="ff8b0-122">Deze code maakt een container en een blob uploadt naar deze container.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="ff8b0-123">`MyClass.cs`moet eruitzien als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="ff8b0-123">`MyClass.cs` should look like hello following:</span></span>

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

<span data-ttu-id="ff8b0-124">Zorg ervoor dat tooreplace 'your_account_name_here' en 'your_account_key_here' werkelijke accountnaam en accountsleutel van uw.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-124">Make sure tooreplace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="ff8b0-125">Uw iOS-, Android en Windows Phone-projecten alle verwijzingen tooyour draagbare project hebben-wat betekent dat u alle gedeelde code kunt schrijven in een plaats en deze gebruiken voor alle projecten.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-125">Your iOS, Android, and Windows Phone projects all have references tooyour Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="ff8b0-126">Nu kunt u de volgende regel code tooeach project toostart profiteert Hallo toevoegen:`MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="ff8b0-126">You can now add hello following line of code tooeach project toostart taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="ff8b0-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="ff8b0-127">XamarinApp.Droid > MainActivity.cs</span></span>

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

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="ff8b0-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="ff8b0-128">XamarinApp.iOS > ViewController.cs</span></span>

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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="ff8b0-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="ff8b0-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

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

## <a name="run-hello-application"></a><span data-ttu-id="ff8b0-130">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ff8b0-130">Run hello application</span></span>
<span data-ttu-id="ff8b0-131">U kunt deze toepassing nu uitvoeren in een Android- of Windows Phone-emulator.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="ff8b0-132">U kunt deze toepassing ook uitvoeren in een iOS-emulator, maar hiervoor moet een Mac.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="ff8b0-133">Voor specifieke instructies over hoe toodo, documentatie te lezen Hallo voor [verbinding maken met Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="ff8b0-133">For specific instructions on how toodo this, please read hello documentation for [connecting Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="ff8b0-134">Als u uw app hebt uitgevoerd, Hallo-container gemaakt wordt `mycontainer` in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-134">Once you run your app, it will create hello container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="ff8b0-135">Hallo-blob bevatten moeten `myblob`, die de tekst hello, heeft `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-135">It should contain hello blob, `myblob`, which has hello text, `Hello, world!`.</span></span> <span data-ttu-id="ff8b0-136">U kunt dit controleren met behulp van Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="ff8b0-136">You can verify this by using hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff8b0-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ff8b0-137">Next steps</span></span>
<span data-ttu-id="ff8b0-138">In deze zelfstudie hebt u geleerd hoe een toepassing platformoverschrijdende in Xamarin toocreate die gebruikmaakt van Azure Storage, specifiek gericht op een scenario in Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-138">In this tutorial, you learned how toocreate a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="ff8b0-139">Echter, u kunt doen veel meer met niet alleen de Blob-opslag, maar ook met tabel-, bestands- en Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="ff8b0-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="ff8b0-140">Kijk eens Hallo artikelen toolearn meer te volgen:</span><span class="sxs-lookup"><span data-stu-id="ff8b0-140">Please check out hello following articles toolearn more:</span></span>

* [<span data-ttu-id="ff8b0-141">Aan de slag met Azure Blob Storage met .NET</span><span class="sxs-lookup"><span data-stu-id="ff8b0-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="ff8b0-142">Aan de slag met Azure Table Storage met .NET</span><span class="sxs-lookup"><span data-stu-id="ff8b0-142">Get started with Azure Table storage using .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="ff8b0-143">Aan de slag met Azure Queue Storage met .NET</span><span class="sxs-lookup"><span data-stu-id="ff8b0-143">Get started with Azure Queue storage using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="ff8b0-144">Aan de slag met Azure File Storage in Windows</span><span class="sxs-lookup"><span data-stu-id="ff8b0-144">Get started with Azure File storage on Windows</span></span>](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]


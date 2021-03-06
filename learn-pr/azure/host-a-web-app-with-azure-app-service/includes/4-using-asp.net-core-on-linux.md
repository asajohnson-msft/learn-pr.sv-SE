Du har valt att använda en teknik med öppen källkod för att skapa ditt webbprogram. Du vet att ASP.NET Core är ett plattformsoberoende ramverk med öppen källkod. Du bestämmer dig för att utveckla din webbapp i en Linux-utvecklingsmiljö med hjälp av ASP.NET Core!

Med Azure App Service kan du använda valfri webbteknik, till exempel Node.js, PHP eller .NET Core.

Här lär du dig hur du skapar ett ASP.NET Core-program med hjälp av .NET-kommandoradsgränssnittet.

## <a name="what-is-aspnet-core"></a>Vad är ASP.NET Core?

ASP.NET Core är den senaste utvecklingen av Microsofts populära ASP.NET-webbramverk. Ett plattformsoberoende ramverk med öppen källkod för utveckling av moderna, molnbaserade och internetanslutna program.

ASP.NET Core-program kan skrivas mot .NET Core Framework eller det befintliga, fullständiga .NET Framework-ramverket.

Eftersom ASP.NET Core är ett plattformsoberoende ramverk med öppen källkod kan du skapa ASP.NET Core-appar på en rad olika plattformar, inklusive Windows, macOS och Linux. Microsoft erbjuder Visual Studio IDE för både Windows- och macOS-miljöer. Och Visual Studio Code-redigeraren är plattformsoberoende och kompatibel med dessa samt Linux.

>För att ge stöd för utveckling av ASP.NET Core-program på olika plattformar introducerade Microsoft .NET Core CLI-verktygen som hjälper dig att bygga, testa och publicera dina program med hjälp av funktionsrika, enhetliga och plattformsoberoende API:er.

Med ASP.NET Core kan du skapa webbappar och tjänster, IoT-appar och mobila serverdelar. ASP.NET Core-program kan köras antingen i molnet eller lokalt.

ASP.NET Core består av en inbäddad webbserver och en körningsmiljö som kör programkoden. Programkoden skrivs med hjälp av ett omarbetat ASP.NET MVC-ramverk, som kräver mindre moduler och paket. Resultatet är en mindre ”skiss”, eller blueprint, av webbprogrammet, som enkelt kan underhållas och hanteras i molnmiljöer. Följande bild visar ett ASP.NET Core-program som finns i .NET Core och den externa webbservern som hanterar HTTP-internettrafik.

![På bilden visas ett ASP.NET Core-program och dess körningsmiljö.](../media/4-asp-net-core-architecture.png)

ASP.NET Core-program är fristående **konsolprogram** som anropas via **dotnet**-drivrutinsverktyget. ASP.NET Core-program läses inte in i IIS-arbetsprocessen, utan via en inbyggd IIS-modul med namnet **AspNetCoreModule** som kör det externa konsolprogrammet.

## <a name="how-to-create-an-aspnet-core-web-project"></a>Skapa ett ASP.NET Core-webbprojekt

Det finns två vanliga alternativ för att skapa ett nytt ASP.NET Core-projekt:

- Du kan använda Visual Studio-mallar (Windows- och macOS-versioner) för att generera ett nytt projekt. Visual Studio innehåller en mängd olika mallar som du kan använda för att skapa webbprojekt. Du kan exempelvis använda mallen **Tom** för att skapa ett tomt ASP.NET Core-projekt med baskonfigurationen. Du kan också använda mallen **Webbprogram (Modal-View-Controller)** för att generera ett fullständigt ASP.NET Core MVC-program med **exempelkontroller** och **exempelvyer**som hjälper dig att börja koda ditt program. Det senaste tillskottet är projektmallen **Webbprogram** som används för att skapa ett ASP.NET Core-projekt baserat på Razor-sidor i stället för den traditionella MVC-projektstrukturen.

- Du kan använda kommandoradsgränssnittsverktygen (CLI) för .NET Core för att generera ett nytt ASP.NET Core-projekt. Microsoft har en uppsättning ASP.NET Core-projektmallar för CLI-verktyg som är nästan identiska med Visual Studio-mallarna. Den enda skillnaden med CLI-verktygen är att du måste ange kommandon för att skapa ett nytt ASP.NET Core-projekt.
> .NET CLI-verktygen använder **mallmotorn** för att skapa stöd för olika projektmallar.  Mer information finns på GitHub-lagringsplatsen för [mallmotorn](https://github.com/dotnet/templating) som används internt av .NET CLI-verktygen.

De är de vanligaste verktygen för att skapa ASP.NET Core-projekt. Men det finns fler tillgängliga verktyg som du kan söka efter och utforska.

Det är värt att nämna att projekten som genereras av de olika verktygen kan skilja sig åt en aning, men alla skapar giltiga och optimerade ASP.NET Core-projekt.

## <a name="net-cli-tools"></a>.NET CLI-verktyg

.NET CLI-verktyget, även kallat .NET Core CLI, är ett plattformsoberoende verktyg som tillhandahåller kommandon för att skapa och återställa paket, och för att utveckla, köra och publicera .NET-program från kommandoraden utan behov av en fullständig IDE-miljö.

.NET CLI installeras som en del av .NET Core SDK. Flera versioner av CLI kan finnas samtidigt på samma dator och köras parallellt.

Om du utvecklar lokalt behöver du, för att börja använda .NET-CLI, installera relevant .NET Core SDK. Azure Cloud Shell har redan .NET CLI-verktyget installerat.

Öppna kommandotolken och skriv följande:

```console
dotnet --version
```

Det här kommandot visar den version av .NET-CLI som är installerad.

För denna skrift kommer en körning av Azure Cloud Shell att returnera: `2.0.0`. Det finns nyare versioner och du kan ha en nyare version på den lokala datorn.

Låt oss börja med att utforska några av de populära kommandona av .NET-CLI.

Kommandot *dotnet* har följande allmänna syntax:

```console
dotnet [verb] [arguments]
```

Verbet som representerar åtgärden som ska köra. Argumenten representerar listan med indataargument som verbet kräver för att kunna köras.

Om du vill ha hjälp med att använda *dotnet* och visa en lista över de tillgängliga *verben* och annan relaterad information, skriver du följande kommando:

```console
dotnet --help
```

Det här kommandot visar följande:

```console
.NET Command Line Tools (2.1.302)
Usage: dotnet [runtime-options] [path-to-application]
Usage: dotnet [sdk-options] [command] [arguments] [command-options]

path-to-application:
  The path to an application .dll file to execute.

SDK commands:
  new              Initialize .NET projects.
  restore          Restore dependencies specified in the .NET project.
  run              Compiles and immediately executes a .NET project.
  build            Builds a .NET project.
  publish          Publishes a .NET project for deployment (including the runtime).
  test             Runs unit tests using the test runner specified in the project.

...
```

Under **SDK commands** kan du se hela listan med kommandon som du kan köra mot .NET Core SDK.

De mest användbara kommandona som ofta används är följande:

- **dotnet new**: Det här kommandot används för att bygga/generera ett nytt .NET-program.

- **dotnet restore**: Det här kommandot används för att återställa/hämta alla paket som programmet refererar till.

- **dotnet run**: Det här kommandot används för att köra .NET-programmet.

Om du vill ha hjälp med att använda ett visst kommando kan du skriva följande:

```console
dotnet new --help
```

Det här kommandot resulterar i:

```console
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.
  -n, --name          The name for the output being created. If no name is specified, the name of the current directory is used.
  -o, --output        Location to place the generated output.
  -i, --install       Installs a source or a template pack.
  -u, --uninstall     Uninstalls a source or a template pack.
  --nuget-source      Specifies a NuGet source to use during install.
  --type              Filters templates based on available types. Predefined values are "project", "item" or "other".
  --force             Forces content to be generated even if it would change existing files.
  -lang, --language   Filters templates based on language and specifies the language of the template to create.


Templates                                         Short Name         Language          Tags
----------------------------------------------------------------------------------------------------------------------------
Console Application                               console            [C#], F#, VB      Common/Console
Class library                                     classlib           [C#], F#, VB      Common/Library
...

Razor Page                                        page               [C#]              Web/ASP.NET
MVC ViewImports                                   viewimports        [C#]              Web/ASP.NET
MVC ViewStart                                     viewstart          [C#]              Web/ASP.NET
ASP.NET Core Empty                                web                [C#], F#          Web/Empty
ASP.NET Core Web App (Model-View-Controller)      mvc                [C#], F#          Web/MVC
ASP.NET Core Web App                              razor              [C#]              Web/MVC/Razor Pages
ASP.NET Core with Angular                         angular            [C#]              Web/MVC/SPA
...

Solution File                                     sln                                  Solution

Examples:
    dotnet new mvc --auth Individual
    dotnet new webapi
    dotnet new --help
```

Det här kommandot visar de tillgängliga alternativen som du kan använda med kommandot `dotnet new`. Det visar även alla tillgängliga projektmallar som du kan använda för att skapa ditt .NET-program. Slutligen finns ett avsnitt som visar exempel på hur du använder kommandot för att skapa ett nytt .NET-program.

Du kan lära dig mer om resten av kommandona genom att använda argumentet `--help` med valfritt kommando som är tillgängligt i .NET CLI.

## <a name="summary"></a>Sammanfattning

När du har bestämt dig för att skapa ett webbprogram kan du välja mellan flera språk och ramverk. I App Service blir valet enklare eftersom du kan använda olika typer av program, till exempel Node.js, PHP eller .NET Core. På så sätt kan du använda de språk och ramverk som du är mest bekväm med i stället för att behöva anpassa dig efter webbvärdens krav.

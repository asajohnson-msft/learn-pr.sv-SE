Du har skapat en webbplats är redo att distribuera den till Azure. Nu behöver vi överväga vilka Azure-tjänster som bäst passar våra behov. Med Web Apps får du en mycket skalbar och automatiskt uppdaterad webbvärdtjänst för dina program.

Här kan titta vi på hur du använder Visual Studio för att publicera ditt ASP.NET Core-webbprogram till en Azure App Service-plan

## <a name="azure-subscription"></a>Azure-prenumeration

För att publicera till Azure behöver du ha en Azure-prenumeration. Du kan använda en [kostnadsfri Azure-prenumeration](https://azure.microsoft.com/free/) för att testa Azure App Service-funktionerna.

## <a name="what-are-web-apps"></a>Vad är Web Apps?

Azure App Service Web Apps (Web Apps) är en tjänst som kan användas som värd för webbprogram, REST API:er och mobila serverdelar. Web Apps är värd för kod som skrivs i olika språk, till exempel .NET, .NET Core, Java, Ruby, Node.js, PHP och Python. Web Apps är utmärkt för de flesta webbplatser, särskilt om du inte behöver stor kontroll över den värdbaserade infrastrukturen.

## <a name="what-is-the-app-service-plan"></a>Vad är App Service-planen?

App Service-planen definierar de beräkningsresurser som din app kommer att använda, var de resurserna finns, hur många ytterligare resurser som planen kan använda samt typen av den serviceplan som används. Dessa beräkningsresurser motsvarar servergruppen i konventionella webbvärdtjänster. En eller flera appar kan konfigureras för att köras på samma App Service-plan.

När du distribuerar dina appar kan du skapa en ny App Service-plan, eller så kan du fortsätta att lägga till appar i en befintlig plan.  Dock delar alla appar i samma App Service-plan samma beräkningsresurser. För att avgöra om den nya appen har de resurser som krävs måste du känna till kapaciteten för den befintliga App Service-planen och den förväntade belastningen för den nya appen. Om en App Service-plan överbelastas kan det eventuellt medföra driftstopp för dina nya och befintliga appar.

Du kan definiera en App Service-plan i förväg i Azure-portalen med PowerShell eller Azure CLI, eller konfigurera en när du publicerar ditt program i Visual Studio.

Varje App Service-plan definierar:

- Region (USA, västra, USA, östra osv.)
- Antal VM-instanser
- Storleken på VM-instanser (liten, medel, stor)
- Prisnivå (Kostnadsfri, Delad, Basic, Standard, Premium, PremiumV2, Isolerad, Förbrukning)

## <a name="specify-the-region"></a>Ange region

När du skapar en App Service-plan måste du definiera en region eller en plats där planen kommer att finnas. Vanligtvis väljer du en region som är geografiskt nära dina förväntade kunder.

## <a name="what-are-the-pricing-and-reliability-levels"></a>Vilka är pris- och tillförlitlighetsnivåerna?

En viktig faktor när du distribuerar appar till Azure App Service är att välja rätt serviceplan. App Service-planen kan skalas upp eller ned när som helst. Du kan välja en lägre prisnivå först och skala upp senare när du behöver fler App Service-funktioner.

Det finns ett antal kategorier för prisnivåer:

**Delad beräkning**: **Kostnadsfri och Delad**, de två grundläggande nivåerna, kör en app på samma virtuella Azure-dator som andra App Service-appar, inklusive appar för andra kunder. Dessa nivåer allokerar CPU-kvoter till varje app som körs på de delade resurserna, och de resurserna kan inte skala ut.

Planerna Kostnadsfri och Delad passar bäst för småskaliga personliga projekt med mycket begränsade trafikkrav, med en angiven gräns på 165 MB utgående data var 24:e timme.

**Dedikerad beräkning**: nivåerna **Basic, Standard, Premium och PremiumV2** kör appar på dedikerade virtuella Azure-datorer. Det är bara appar i samma App Service-plan som delar samma beräkningsresurser. Ju högre nivå, desto fler VM-instanser blir tillgängliga som du kan skala ut.

Serviceplanen Standard är bäst lämpad för arbetsbelastningar som är live i produktion, där du publicerar kommersiella program till kunder.
Premium-serviceplanerna stöder webbappar med hög kapacitet där du vill undvika de ytterligare kostnaderna för en dedikerad (isolerad) plan.

**Isolerad**: den här nivån kör dedikerade virtuella Azure-datorer på dedikerade virtuella Azure-nätverk, vilket ger nätverksisolering ovanpå beräkningsisolering till dina appar. Den ger maximalt med utskalningsfunktioner. Du väljer bara serviceplanen Isolerad om du har specifika krav på högsta möjliga säkerhet och prestanda.

Isolera din app till en ny App Service-plan när:

- Appen är resurskrävande
- Du vill skala appen oberoende av de andra apparna i den befintliga planen
- Appen behöver resurser i en annan geografisk region

**Förbrukning**: den här nivån är endast tillgänglig för funktionsappar. Den skalar funktionerna dynamiskt beroende på arbetsbelastningen. Mer information finns i jämförelsen av Azure Functions-värdplaner.

## <a name="specify-the-resource-group"></a>Ange resursgruppen

Som med de flesta Azure-resurser behöver du ange den resursgrupp som du vill använda. Du kan använda en använda en befintlig resursgrupp eller skapa en ny direkt från Visual Studio. En resursgrupp är en logisk container som Azure-resurser (t.ex. webbappar, databaser och lagringskonton) distribueras och hanteras i. Det är en användbar mekanism för att hålla associerade resurser tillsammans.

## <a name="deploy-your-web-app-from-visual-studio"></a>Publicera webbappen från Visual Studio

Det är en kort process att publicera din app till Azure från Visual Studio.

### <a name="select-the-project"></a>Välj projektet

1. Högerklicka på projektet i Solution Explorer.
1. Välj **Publicera > Publicera till Azure**

### <a name="configure-the-app-service-plan-in-windows"></a>Konfigurera App Service-planen i Windows

1. Konfigurera App Service-planen
    - Värd: du konfigurerar din App Service-plan på den här fliken. Den anger plats, storlek och funktioner för den webbserver som är värd för din app. Du kan välja en befintlig värdplan eller skapa en ny. Windows genererar automatiskt globalt unika namn som du kan ändra under konfigurationen.
    - Tjänster: du kan konfigurera en SQL-databas för webbplatsen här.

        > [!NOTE]
        > Du kan ansluta och hantera en SQL-databas i Azure från Visual Studio, men det ligger utanför omfånget för den här modulen.

1. Klicka på Skapa för att distribuera appen. När det är klart startar Visual Studio den webbsida som är värd för din webbplats.

### <a name="configure-the-app-service-plan-for-mac"></a>Konfigurera App Service-planen för Mac

1. Du kan välja en befintlig App Service-plan om du har en konfigurerad i Azure eller skapar en ny
1. Konfigurera din App Service-plan på den här fliken. Den anger plats, storlek och funktioner för den webbserver som är värd för din app. Du kan välja en befintlig värdplan eller skapa en ny. Kom ihåg att Azure kräver att namnen på din webbplats och alla resurser är globalt unika.
1. Klicka på Skapa för att distribuera appen. När det är klart startar Visual Studio den webbsida som är värd för din webbplats.

## <a name="summary"></a>Sammanfattning

ASP.NET Core-webbprogram och Azure App Services ger en flexibel och skalbar lösning som värd för din ASP.NET-webbapp. Som med alla Azure-tjänster behöver du ange en resursgrupp och välja den prisnivå som bäst uppfyller dina behov.
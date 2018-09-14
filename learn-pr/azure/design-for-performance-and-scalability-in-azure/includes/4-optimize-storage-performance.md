Det är viktigt att du överväger lagringsprestandan i din arkitektur. Dålig prestanda på lagringsnivå kan påverka slutanvändarna precis som långa svarstider i nätverket. Hur kan du optimera din datalagring? Vad behöver du tänka på så att du inte inför flaskhalsar för lagringen i arkitekturen? Nu ska vi gå igenom hur du kan optimera lagringsprestandan i din arkitektur.

## <a name="optimize-virtual-machine-storage-performance"></a>Optimera lagringsprestandan för virtuella datorer

Först tittar vi på hur du kan optimera lagringen för virtuella datorer. Disklagringen spelar stor roll för prestandan i dina virtuella datorer, så det är viktigt att välja rätt typ av diskar för appen.

Olika appar har olika krav på lagringen. Appen kan vara känslig för svarstider vid läs- och skrivåtgärder, eller så kan den behöva hantera stora IOPS-volymer eller helt enkelt stora dataflöden.

Vilken typ av disk ska du använda när du skapar en IaaS-arbetsbelastning? Det finns fyra alternativ:

- **Lokal SSD-lagring** – varje virtuell dator har en tillfällig disk som backas upp av lokal SSD-lagring. Storleken på disken varierar beroende på den virtuella datorns storlek. Eftersom den här disken är en lokal SSD-disk har den bra prestanda, men data kan förloras vid underhåll eller om den virtuella datorn distribueras om. Den här typen av disk passar endast för tillfällig lagring av data som du inte behöver permanent. Den här disken är utmärkt för växlingsfiler och exempelvis tempdb i SQL Server. Den här lagringen är kostnadsfri. Den ingår i kostnaden för den virtuella datorn.

- **Standardlagring HDD** – det här är spindeldisklagring som kan passa bra när appen inte är känslig för varierande svarstider eller dataflöden. Ett bra exempel är en arbetsbelastning för utveckling/testning där du inte behöver garanterade prestanda.

- **Standardlagring SSD** – det här är SSD-lagring med korta svarstider men för mindre dataflöden. Den här disktypen kan passa bra för webbservrar utanför produktion.

- **Premiumlagring SSD** – Den här SSD-lagringen passar bra till arbetsbelastningar som används i produktion, där du behöver bästa möjliga tillförlitlighet, korta svarstider samt stora dataflöden och IOPS-volymer. Eftersom de här diskarnas prestanda och tillförlitlighet är bättre rekommenderas de för alla arbetsbelastningar i produktion.

Premiumlagring kan bara kopplas till virtuella datorer av vissa storlekar. Premium storage kan storlekar betecknas med en ”s” i namnet, till exempel D2**s**_v3 eller Standard_F2**s**_v2. Du kan koppla HDD- eller SSD-diskar av standardtyp till valfri virtuell dator (med eller utan s i namnet).

Du kan koppla diskar med en stripeteknik (som Lagringsdirigering i Windows eller mdadm i Linux) om du behöver hantera större dataflöden och IOPS-volymer, genom att diskaktiviteten sprids ut över flera diskar. När du stripekopplar diskarna kan du verkligen få ut mesta möjliga av diskarna, och det här är vanligt i avancerade databassystem och andra system med stora lagringskrav.

När du använder arbetsbelastningar i virtuella datorer måste du utvärdera appens prestandakrav så att du vet hur mycket underliggande lagring du måste etablera för de virtuella datorerna.

## <a name="optimize-storage-performance-for-your-application"></a>Optimera lagringsprestanda för appen

Även om du kan använda olika lagringstekniker för att förbättra diskens prestanda kan du även påverka prestandan för dataåtkomsten på programnivå. Nu ska vi gå igenom hur du kan göra det.

### <a name="caching"></a>Cachelagring

Ett vanligt sätt att förbättra appars prestanda är att integrera ett cachelager mellan appen och ditt datalager. Vid cachelagring lagras data normalt i minnet så att de snabbt kan hämtas. Det här kan vara data som används ofta, data du anger från en databas eller tillfälliga data som användarnas tillstånd. Du har kontroll över vilken typ av data som lagras, hur ofta den uppdateras och när den upphör att gälla. Genom att placera den här cachelagringen i samma region som appen och databasen minskar du svarstiderna mellan dem. Det är nästan alltid snabbare att hämta data från cachelagringen än att hämta samma data från en databas, så med ett cachelager kan du förbättra appens prestanda avsevärt. Följande bild visar hur ett program hämtar data från en databas, lagrar den i ett cacheminne och använder det cachelagrade värdet efter behov.

![En bild som visar att hämta data från cachen är snabbare än att hämta från en databas.](../media/4-cache.png)

Azure Redis Cache är en cachelagringstjänst i Azure. Den baseras på Redis Cache (öppen källkod). Azure Redis Cache är en helt hanterad tjänst som Microsoft erbjuder. Du väljer vilken prestandanivå du behöver och konfigurerar appen för användning av tjänsten.

### <a name="polyglot-persistence"></a>Flerspråkig persistens

Flerspråkig persistens är när du använder olika lagringstekniker för lagring av olika datatyper.

Tänk dig t.ex. en onlinebutik. Du kan lagra appresurser i bloblagring, produktrecensioner och rekommendationer i ett NoSQL-lager och användarprofiler eller kontouppgifter i en SQL-databas. Följande bild visar hur ett program kan använda flera tekniker för lagring av data för att lagra olika typer av data.

![En bild som visar användningen av olika Lagringsmetoderna inom samma program att öka prestandan och minska kostnaderna.](../media/4-polyglotpersistence.png)

Det här är viktigt eftersom olika datalager är utformade för olika användningsfall, och kan vara otillgängliga på grund av kostnaderna. Att lagra blobar i en SQL-databas kan vara både dyrare och leda till längre svarstider än att använda dem direkt från bloblagret.

Om du använder många reservlager ökar lösningens komplexitet. Fundera på hur du uppfyller de icke-funktionella kraven med de olika datalagren och hur försämringar i tjänsten påverkar appen som helhet. Tänk även på hur data hålls konsekventa mellan de olika datalagren. 

**Eventuell konsekvens** ger ofta en bra balans, men det finns flera olika konsekvensmodeller beroende på tjänsten.

Eventuell konsekvens innebär att replikdatalagren till slut sammanfogas om inga ytterligare skrivningar görs. Om en skrivning görs till ett av datalagren kan läsningar från ett annat lager visa något inaktuella data. Du kan använda eventuell konsekvens i större skala eftersom läsningar och skrivningar har korta svarstider, på grund av att informationens konsekvens inte måste kontrolleras i alla datalager.

## <a name="lamna-healthcare-example"></a>Lamna Healthcare-exempel

Bokningssystemet för Lamna Healthcares patienter körs i två Azure-regioner, Europa, västra och Australien, östra. De använder virtuella datorer som klientnoder för distribuering av webbplatsen, och de har en Azure SQL DB distribuerad i regionen Europa, västra som primär lagring och regionen Australien, östra som sekundärt läsbart lager. Klientnoderna behöver inge hantera några stora dataflöden, men de behöver korta svarstider och hög tillförlitlighet, så därför används SSD-premiumlagring.

De kör ett Azure Redis Cache lokalt i respektive Azure-region för att lagra vanliga användarförfrågningar och läkarnas tillgänglighet. Cachelagringen är implementerad för att optimera prestandan hos de vanligaste dataläsningsåtgärderna i appen.

## <a name="summary"></a>Sammanfattning

Vi har gått igenom några exempel på hur du kan förbättra lagringsprestanda på infrastrukturnivån genom att välja rätt diskarkitektur, och på programnivå med hjälp av cachelagring och att välja rätt dataplattform för dina data. När du har rätt arkitektur i din lösning garanterar du bästa möjliga prestanda för dina data. Nu ska vi gå igenom hur du kan identifiera prestandaproblem i en arkitektur.
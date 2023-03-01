#Namn: Arman Kamali
Klass : Clo 22
Datum : 2023-03-01


Verktyg som används i detta inlämning är:
Visual Studio Code, PowerShell och Google Drive Dokument
Tjänster som användes i detta inlämning är:
Microsoft Azure och Github
 
Inlämningsuppgift 1

När man är nöjd med sin utveckling, skapar vi server som använder linuxdistributionen Ubuntu som operativsystem samt installera .Net Runtime.
För att skapa en ny Server går vi till →Logga in i  Microsoft Azure → All Services → Virtual machines → Create → Azure virtual machines.
Fylla på Virtual machine Server → Region→ options →  zon → 

väljer man Ubuntu Server … → Sedan man ska välja Size (Standard_B1ls) den billigaste → undvika välja Password → skriv egen Username → SSH public key source lämnar default → Key pair name default (om du vill inte ange namn). 

Öppna port 80 (man kan lämna default alltså det räcker med “SSH(22)” ) → 

Sedan →Next : Disk(lämna default i detta fall) → om du vill inte har fler disk kan du fortsätta → Next : Networking (det är bra att kryssa Delete public.. för att radera public IP när du radera din VM) →   

fortsätt→ NEXT till → create →

 


Sen skapar vi en new Repository i github (MyWeb) → för att clone hem det Repository → kopiera (HTTPS) → 

→ klicka på Clone Git Repository… → krista in HTTPS → Enter

Höger klicka på README → Sedan öppnar vi Terminalen → 

→ skriv följande kommando i Terminalen: 
git clone (krista in HTTPS) 
ls

Sedan för att generera webbapplikationen →skriver följande kommando 
dotnet new webapp  → “skapar webbapplikation”
dotnet run →”för att prova om det fungerar” eller enklast kör kommando 
dotnet watch run 

→ Ctrl+klick

Nu lyssnar det bara på Localhost, vi ska programmera får att få lyssnar på andra portar.
För att göra det → klicka på Program.cs → och skriv → app.Urls.Add(“http://*:5000”); → Spara det → 

kör kommando → dotnet run 

Now listening on : http://[::]:5000 → betyder att den lyssnar på alla portar  →
nu ska vi prova om det funkar genom att surfa → localhost:5000/


Allt är klart för att köra det på servern: 
För att göra det kör vi kommando :
dotnet publish  

Under bin mappen hittar du publish → 
kör kommando för att få info från git→ 
git status

Nu ska vi gå på vår servern och för breddar det  genom att → klicka på din virtual machine → Connect → Kopiera kommando →  

Öppna PowerShell → Kör följande kommando: 
ls
ssh -i <private key path> azureuser@51.120.120.143 (kom ihåg! istället för <private key path> man dra hela dokumenten key från folder och krista in och komma ihåg att ha rätt IP-adress) 
yes


Nästa Steg är att installera .NET R
För att installera .Net Runtime behöver vi följande kommando:
wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
sudo apt-get update && \
  sudo apt-get install -y aspnetcore-runtime-6.0 
kom ihåg:  nu är det “sudo apt-get install -y aspnetcore-runtime-6.0” men du kan välja “…runtime-7.0” istället. beror på vilket variation man använder 
kör kommando för att säkra att den är installerad:
dontnet
dotnet --list-runtimes

Nu ska vi kopiera upp alla filerna använd kommando → vi går tillbaka till visual studio code → Terminal →
ssh -i <private key path> azureuser@51.120.120.143 →(glöm ej ändra key och IP-adress) 

Nästa kommando → 
exit 
Nu kopiera vi alla filerna och lägger på servern, använda “S copy” kommando  → 
scp -i c:\Users\Arman\Downloads\DemoTest1_key.pem azureuser@51.120.120.143 → istället för ssh ← →scp   och sen
Dra in “publish” filen och krista efter “...key.pem” 

Nu kopiera det alla filer som finns i publish katalogen och lägger det i Servern→
För att testa om det klart skriv kommando på PowerShell→ 
ls
cd MyWeb/
ls
dotnet MyWeb.dll

Nu är det en sak kvar, brandväggen(porten) är stängd till servern. För öppna det går vi till → VM → Networking → Add inbound port rule

Nästa steg är att öppna port 5000 → Add

Nu är det port 5000 öppen→

För att testa om det fungerar gå → Overview → kopiera IP-adressen → i det här fallet 51.120.116.102:5000 och sök → 



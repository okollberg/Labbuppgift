# **Labbmiljö, Git, CLI och AI** 

Oscar Kollberg  
2026-09-22  
*Introduktion till yrkesrollen och grunderna inom IT infrastruktur*


**1. Syfte**

Syftet med uppgiften är att få praktisk erfarenhet av Linux, Windows, nätverk och kommandoraden. Tränar även på att dokumentera med Git och använda AI som hjälpmedel samt göra en kritisk granskning av informationen.


**2. Labbmiljö & Nätverk**  

Jag valde att sätta upp min labbmiljö i Oracle Virtualbox. Kör en Linux Ubuntu server samt en windows 11 klient och lägger detta som internt nätverk "Labbmiljö" i Virtualbox
![virtualboxuppsättning](/virtualboxlabb.jpg)
  


| Hostname | Operativsystem | Ip address | Subnätmask | Standard gateway |  
|---|---|---|---|---|
| labb-winclient | Windows 11 | 192.168.10.20 | 255.255.255.0 | Ingen |
| labb-server |  Ubuntu server | 192.168.10.10 | 255.255.255.0 | Ingen |

Tilldelat IP-adress till Windows via powershell: New-NetIPAddress -InterfaceAlias "Ethernet" -IPAddress 192.168.10.20 -PrefixLength 24

Tilldelat IP-adress till Ununtu via terminal där jag konfigurerade i netplan-filen med:
sudo nano /etc/netplan/00-installer-config.yaml

![ipinställning linux](/iplinux.jpg)

Testade sedan att pinga mellan klienterna. Jag stötte dock på problem då Windows brandväggen blockerade ping. Detta löste jag genom att lägga in en regel i Windows brandväggen. Efter det fungerade det att pinga. 

**3. Kommandoradsgenomförande**  


*Linux*

1. Började med att skapa mappen /var/systementor/konsultdata med kommandot:   
  
    sudo mkdir -p /var/systementor/konsultdata  
    (Angav det först utan sudo men upptäckte att jag behövde root rättigheter.)  
    ![konsultdatamapp](/Linux1.png)  

    Skapade sedan .txt filen med sudo touch /var/systementor/konsultdata/anteckningar.txt  

    ![filenanteckningar](/Linux1.2.png)  
    
2. Skapar ny användargrupp med kommandot:  

    sudo groupadd konsulter    
    ![groupaddkonsulter](/Linux2.png)  

3. Tilldelar mappen och filen till gruppen konsulter med sudo chown och kollar sedan behörigheterna med ls -la

    sudo chown :konsulter /var/systementor/konsultdata  
    sudo chown :konsulter /var/systementor/konsultdata/anteckningar.txt
    ![grupptilldelning](/Linux3.png)  
      
      Efter detta ändrar jag behörigheterna med chmod 750 och chmod 640  
        
    ![behörigheter](/Linux3.2.png)

4. Kollar behörigheterna med ls -la

    ![behörigheter](/Linux4.png)
  
    Där kan man se att ägare har rättigheter att göra allt. Gruppen får r-x på mappen men får inte skriva (w). På .txt filen har konsulter bara rätt att läsa (r)

5. Pingar Windows klienten som har 192.168.10.20
  
    ![pingarwindows](/Linux5.png)  

    Nätverkskortets detaljer (ip addr show)

    ![nätverkskortdet](/Linux5.2.png)

*Windows*

1. Skapar mappen och undermappar med new-item -itemtype directory -path c:\systementor\konsultdata

    ![skapamappwindows](/Windows1.png)

2. Jag använde $acl = get-acl c:\systementor\konsultdata för att hämta behörighetsstrukturen och spara den i variabel $acl. Använde sedan $acl.access för visa behörighetsstrukturen i variabeln.

    ![aclbehörighetsstruktur](/Windows2.png)

3. Pingar Linux servern som har 192.168.10.10

    ![pinglinux](/Windows3.png)

    Inspekterar nätverksinställningarna med ipconfig /all

    ![ipconfigwindows](/Windows3.2.png)

**4. Git & Versionshantering**  

Länk till Git repository https://github.com/okollberg/Labbuppgift



**5. AI-logg och utvärdering**  

Jag valde att be ChatGPT att förklara bash kommandot chmod och fick då detta AI-utdata:

![chmod1](/chmod1.png)
![chmod2](/chmod2.png)
![chmod3](/chmod3.png)
![chmod4](/chmod4.png)

Jag upplever att svaret var tydligt och gick igenom steg för steg hur man använder kommandot för att ändra behörigheter. Man fick svar på vad de olika rättigheterna innebär och hur man använder både symboler och det oktala systemet.
Man får även förklaring på hur man använder chmod -R för att ändra behörigheten recursivt när man sätter behörighet på en katalog som innehåller fler kataloger eller filer. 
Däremot får man ingen tydlig förklaring på vad som händer med nya filer och kataloger som läggs till efter man ändrat behörighet på katalogen.

Jag testade därför av det med att skapa en katalog med en fil i, ändrade behörighet på katalogen och dess innehåll. Därefter skapade jag en ny fil. Där kan man se att filen inte fick samma behörigheterna man tidigare satt.

![chmodtest](/chmodtest.png)

Jag kan inte se några föråldrade kommandon eller hallucinationer. Däremot så har man inte riktigt fått all information så det är alltid viktigt att kolla igenom AI-utdatan och ställa följdfrågor.
# **Labbmiljö, Git, CLI och AI** 

Oscar Kollberg  
2026-09-14  
*Introduktion till yrkesrollen och grunderna inom IT infrastruktur*


**1. Syfte**

Syftet med denna labb är att sätta upp ett virtuellt nätverk där man använder både Linux och windows. Konfigurera nätverket och arbeta med CLI samt dokumentera via git och github


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
Steg-för-steg-dokumentation (med
(CLI-kommandon och skärmdumpar/kodblock) för både Linux och Windows.)

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

**4. Git & Versionshantering**  
Länk till ditt Git-repository samt
utskrift/skärmdump på din git log --online som visar din ändringshistorik.

**5. AI-logg & Reflektion**  
Prompt, AI-utdata och din kritiska granskning.


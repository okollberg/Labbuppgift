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

**3. Kommandoradsgenomförande**  
Steg-för-steg-dokumentation (med
(CLI-kommandon och skärmdumpar/kodblock) för både Linux och Windows.)

**4. Git & Versionshantering**  
Länk till ditt Git-repository samt
utskrift/skärmdump på din git log --online som visar din ändringshistorik.

**5. AI-logg & Reflektion**  
Prompt, AI-utdata och din kritiska granskning.


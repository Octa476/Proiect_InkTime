# Proiect_InkTime
Schematic si PCB design pentru ceasul InkTime in cadrul proiectului de la materia TSC.

## Diagrama Bloc
Diagrama bloc a proietului (o varianta destul de minimala, dar suficienta pentru a intelege cum interactioneaza componentele intre ele) este prezenta in folder-ul root proiectului in varianta HTML si a fost realizata folosind [www.drawio.com](https://www.drawio.com/).

## BOM
Tabelul BOM este este prezent sub format .csb in folder-ul root al proiectului si a fost generat folosind facilitatile fusion autodesk.

## Descrierea functionalitatii hardware
- componente ce folosesc I2C: LiPo Charger, DC/DC, IMU, Fuel Gauge, Haptic
Driver;
- componente ce folosesc SPI: E-Paper Display Connector;
- IMU este un accelerometru, fiind utilizat pentru determinarea acceleratiei pe cele 3 axe;
- LiPo Charger este folosit pentru a incarca bateria;
- DC/DC este un stabilizator de tensiune si este folosit pentru a oferi o tensiune stabila de 3V3 intregii placi;
- nRF52840 este microcontroller-ul placutei si controleaza si orchestreaza intreaga functionalitate a acesteia;
- E-Paper Drive Circuit este folosit pentru a controla display-ul;
- Fuel Gauge este o componenta care indica nivelul de incarcare al bateriei;
- Haptic Driver este folosit pentru a controla vibratia shaker-ului;
- USB C Connector este mufa usb;
- ESD Protection este un modul ce protejeaza placuta de descarcarile elctrostatice ce pot aparea in utilizarea zilnica a ceasului;
- TODO - intelegere mai profunda a schemei electrice si functionalitatii intregului sistem

## Descriere pini nRF52840
- VDD - alimentarea la 3V3
- DCC - 
- DEC4 -
- VSS - GND
- P0.02/AIN0 - SCK - pinul de clock pentru protocolul SPI prin care comunica conectorul de display
- P0.02/AIN0 - MOSI - master output slave in, folosit pentru comunicarea SPI
- DEC2 - GND
- XC2, XC1 - pini pentru sursa de ceas X1 de 32MHz
- DEC3 - GND
- ANT - pin folosit pentru legarea la antena
- P0.10/NFC2 - pin folosit probabil pentru ca Fuel Gauge sa anunte microcontroller-ul cand tensiunea bateriei ajunse sa fie mai mica decat un prag anume
- DEC5 - GND
- SWDIO, SWDCLK, SWO - pini utilizati pentru depanarea si programarea microcontroller-ului
- P.18/RESET - maretul pin de reset
- P0.17, P0.16, P0.15 - pini folositi pentru tranzactionarea cu display-ul
- D-, D+ - pini folositi la tranzactionarea datelor de la USB; folosesc tranmisie diferentiala
- VBUS - alimentarea la 5V a unui USB
- DEC3V3 - GND (ciudat putin)
- P0.12 - enable pentru driverul haptic
- P0.11 - folosit pentru atentiona microcontroller-ul de posibile hazarde de alimentare; este controlar de Lipo Charger
- P1.08, P0.08 - pini de intrerupere pentru modulul de IMU
- P0.07, P0.06 - pini folositi de protocolul I2C
- P0.05/AIN3 - chip select pentru display
- XL2, XL1 - pini pentru sursa de ceas X2 de 32KHz
- DEC1 - GND
- P0.13, P0.14, P1.02 - GPIO's folosite pentru citirea valorii de pe butoane
- am aflat ca pinii de DECx sunt folositi pentru circuitele de regulare a tensiunii din microcontroller (interesant SoC)
- TODO - intelegere mai profunda a schemei electrice si functionalitatii intregului sistem, cu accent pe pinii microcontroller-ului

## Aspecte de design
- am ales sa realizez PCB-ul pe 4 straturi. Am un plan top, unul bottom, un plan de masa pe layer-ul de sub top si un plan de 3V3 pe layer-ul de deasupra lui bottom.
- am pozitionat antena in partea de jos a placii, langa butoane si am decupat PCB-ul sub jumatatea de antena care nu era conectata electric la niciu-un alt fir
- am folosit via in pad si am din aceasta cauza cateva erori pe care le-am acceptat deoarece era singura solutie viabila
- am ales sa am un nivel de detaliu mediu in cadrul modelarii 3D a bateriei, display-ului si shaker-ului
- am conectat shaker-ul si bateria prin fire la test pad-urile asociate lor
- am curbat conectorul flex al display-ului pentru a se potrivi in concectorul de pe PCB folosind comanda bend pentru metal sheets
- am folosit niste inlocuitori pentru modelul 3D al unor piese, deoarece nu am putut identifica un model exact al footprint-ului din schematic sau footprint-ul nu era unul specificat tehnic (ex: PERFECT_0402, JUMPER_SJ, etc)
- am realilzat un exploded view vertical, in care sunt prezente piesele dezasamblate ale ceasului
- am inclus si o animatie pentru exploded view in folder-ul Mechanical
- am inclus cateva screenshot-uri de pe parcursul dezvolatarii proiectului in folderul Images


## Observatii personale
Proiectul a fost extrem de muncitoresc si plin de frustrari din mai multe puncte de vedere. In primul rand, nu am fost "scoliti" in a utiliza la capacitate scazuta spre medie facilitatile de care dispune aplicatia Fusion Autodesk, fapt ce a dus la un loop aproape infinit de vizionat tutoriale si incercari repetate inutile de trage o curba in spatiu pentru desenarea firelor de legatura (un umil exemplu). Mi-as fi dorit ca laboratoarele sa prezinte mai in detaliu functionalitatile esentiale in realizarea proiectului si consider ca nu este o virtute faptul ca ne-am descurcat singuri, deoarece timpul pe care il avem este deja extrem de limitat (da, am invatat multe, pe cont propriu sau prin viu grai, dar ar fi fost mult mai usor sa fim instruiti macar putin mai mult).

Dupa aceasta critica constructiva, as dorii totusi sa felicit ideea de a propune un astfel de proiect. A fost un proces interesant de design, atat la nivel de PCB, cat si modelare 3D, si simt ca m-a ajutat sa ma dezvolt pe plan ingineresc. Am invatat sa ma descurc singur, sa incerc, m-am enervat de multe ori, dar intr-un final am reusit sa fixez un fir exact in pozitia in care imi doream.
Fun fact, am avut un bug in fusion care imi bloca coada de task-uri si ajunsesem sa am in jur de 240 de task-uri in processing, fapt ce imi bloca orice incercare de a exporta un fisier 3D. Din fericire, am rezolvat aceasta problema printr-o comanda text inteligenta.

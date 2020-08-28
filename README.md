
# Primena metoda dubokog ucenja u sintezi sistemi za prepoznavanje lica



### UVOD

Glavni problem koji razmatram u ovom radu jesu komponente koje cine jedan sistem
za prepoznavanje lica. Jos od ranih dana sa pojavom kamera, rodila se potreba za
sistemima koji bi mogli da identifikuju osobe na njima. Tokom vremena su se razne
metode smenjivale, od prepoznavanja pokreta, otisaka prstiju, do prepoznavanja
lica. U ovom radu ce biti reci upravo o tehnologijama koje se koriste za
prepoznavanje lica, konrektno, fokusiracemo se na tehnike dubokog ucenja u sintezi
sistema za prepoznavanje lica. Ovakvi sistemi su slozeni i predstavljaju sintezu
raznih tehnologija i metoda kako bi uspesno radili. Sam razvoj ovih sistema je
zahtevan, i zahteva tim ljudi koji su sposobni za resavanje kako matematickih, tako i
racunarskih problema. Ovi problemi proizilaze iz potrebe za visokom tacnoscu
sistema, kao i od varijacija usled koriscenja razne opreme i alata. Svakoga dana se
sve vise softvera zasniva upravo na ovoj tehnologiji, a to podrazumeva njenu
ispravnost, robusnost i tacnost. Jedna od tehnika koja je omogucila nagli razvoj ove
oblasti jesu duboke neuronske mreze. Pored ovoga, ubrzan razvoj tehnologija i
racunarskih komponenti omogucili su znatno brzi razvoj i treniranje ovakvih mreza, o
cemu ce biti reci u nastavku ovog rada.
Glavni cilj mog istrazivanja u ovom radu jeste sinteza sistema za prepoznavanje lica
koristeci vec postojece metode za detekciju, ekstrakciju vektora obelezja, i njihovo
uporedjivanje radi dobijanja zelenih rezultata.
U svom radu koristicu analiticke metode kako bi svaku celinu razlozio na delove i
bolje objasnio. Sam sistem za prepoznavanje lica je jedna slozena celina koja
ukljucuje delove koji su se godinama razvijali i istrazivali. Ovo znaci da se
kombinacijom ovih podsistema mogu dobiti novi sistemi sa specificnom namenom ili
performansama. Ovi delovi u prokucionom sistemu ne mogu da rade jedan bez
drugog, dok se je prilikom istraizivanja moguce preskociti neke od njih. Uzmimo za
primer detekciju lica. Ukoliko je cilj sistema samo prepoznavanje, a za testiranje,
razvoj i upotrebu se koriste slike koji sadrze samo detektovana lica, onda se sam
korak detekcije moze preskociti. S obzirom na to da ovo cesto nije slucaj,
fokusiracemo se na sintezu kompletog sistema.
U cilju uporedjivanja performansi sa javno dostupnim rezultatima koristicemo setove
podataka koji su opsteprihvaceni u ovoj oblasti. Ovo nam omogucava realniju sliku o
performansama sistema. Dodatno, koristicemo podatke koji nisu cesto korisceni, ali
su javno dostupni. Rec je o slikama koje na prvi pogled coveku deluju tesko za
prepoznavanje. Kao treci nacin testiranja, bice koriscena kamera i snimak sa iste
kako bi videli ponasanje sistema u realnom vremenu. Kod komercijalnih sistema je
ovo kljucan korak gde moze doci do velikih gresaka. Uzmimo za primer dve osobe


koje su jedna pored druge, setaju i okrecu se. Ukoliko se prepoznavanje ne radi u
svakom frame-u, moze doci do zamena njihovoh identiteta prilikom pracenja ukoliko
ovo nije odradjeno na pravi nacin.

## 1.Pregled sistema

Analiza lica predstavlja jedan od bitnih procesa u nasim zivotima. Ljudi analizom lica
prikupljaju bitne podatke o drugim osobama. Ovo ukljucuje podatke o broju godina,
polu, rasnoj pripadnosti. Takodje mozemo prepoznati da li je osoba srecna ili tuzna,
ili pak neku drugu emociju. Pokreti usana su vazni u oblasti prepoznavanja govora,
kao i sve popularnijoj oblasti kao sto je generisanje laznih snimaka. Metode analize
lica nam mogu reci gde je usmeren pogled neke osobe, odnosno sta privlaci njenu
paznju, i ovo moze biti posebno interesantno u marketingu i sopovima, kazinima. U
medicini ove metode mogu biti od koristi za prepoznavanje nekih bolesti, poput
autizma koji se odlikuje time sto osobe imaju poteskoca da iskazu svoje emocije.
Sve navedene metode koriste kako ljudi, tako i racunari.
U ovom radu cemo se fokusirati na metode koje se koriste u procesu detekcije lica,
njegove ekstrakcije, obrade i zatim prepoznavanja.
Na pocetku ovog rada je prvo bitno da uvrdimo sta je zapravo prepoznavanje lica.
Svaka osoba ima karakteristicno lice, i to je ono sto nas cini unikatnima. Vecina
metoda se bazira upravo na ovoj cinjenici, i njihov cilj je ekstrakcija ovih obelezja
(features) za svaku osobu, a zatim i njihova klasifikacija na osnovu odredjenih
parametara.
Treba razlikovati algoritme za prepoznavanje po vise kriterijuma. Osnovna
klasifikacija je na algoritme zasnovane na geometri (Geometry based) i algoritme
zasnovane na sablonima (template based). Geometrijski zasnovani algoritmi
analiziraju odredjena podrucja i geometrijske veze na njima. Zbog ovoga su i poznati
kao algoritmi zasnovani na obelezjima (feature). Sa druge strane su algoritmi
zasnovani na sablonima, i u ovu grupu spadaju: metoda nosecih vektora (SVM),
analiza glavnih komponenti (PCA), linearna diskriminantna analiza (LDA), kernel
metode i jos mnogo drugih.


### RetinaFace

Prvi korak u procesu prepoznavanja lica je njegova detekcija. Osnovna ideja procesa
detekcija je pronalazenje svih lica na slici, odnosno njihovih koordinata. Ove koordinate
sluze za ekstrakciju lica sa slike, te se u nastavku radi samo sa slikama koje sadrze lice.
Takodje se vrlo cesto koordinate cuvaju ukoliko je rec o radu sa video snimcima radi
iscrtavanja. Pored ovog, cuvanje originalne slike i koordinata (bounding box-a ili bbox-a)
imamo mogucnost ponovne ekstrakcije lica sa raznim scale faktorima. Sto moze biti korisno
kao ulaz u neke druge neuronske mreze. Primer ovoga su anti-spoofing mreze koje imaju za
cilj predikciju da li osoba na slici ili snimku prava (real) ili lazna (fake).
Postoji zaista veliki broj razvijenih ideja i projekata na temu detekcije, kako objekata, tako i
lica. Jedna implementacija se izdvaja od drugih, rec je o RetinaNet mrezi. Ovde je rec o
RetinaNet mrezi, dok ce u nastavku biti reco o RetinaFace-u. Razlika je u tome sto je
RetinaNet prva imlementacija koja je namenjena generalno detekciji objekata.
Osnovna ideja sa Retina detektorom je bila u uraditi sve predickije u jednoj fazi. U 2019.
godini, state-of-the-art (SOTA) detektori su bili bazirani na mehanizmu sa dva faze
(takozvani two-stage). Prva faza je podrazumevala generisanje skupa kandidata za lokaciju
na kojoj je moguce naci trazeni objekat, dok se u druga faza sastoji iz klasifikacije svakog
kandidata u jednu od klasa.
RetinaNet je jednofazni (single stage) detektor koji se sastoji jedne mreze (bacbone) i dve
mreze sa specificnom funkcijom. Kao backbone se moze koristiti bilo koja od poznathih
arhitektura (VGG, MobileNet, ResNet) i osnovni cilj ove mreze je racunanje konvolucione
feature mape. Nakon toga, prva podmreza radi klasifikaciju na osnovu izlaza backbone
mreze, dok druga podmreza proracunava bounding box regresiju.
Pored toga sto je ovaj detektor bio single stage, podrzavao je koncept piramida. RetinaNet je
zasnovan na konceptu feature piramida (Feature Pyramid Network - FPN). Ovo je
omoguceno koriscenjem FPN mreze kao backbone mreze. Osnovni princip rada je da FPN
mreza radi augmentaciju standardne konvolucione mreze sa vrha ka dnu sa lateralnim
konekcijama (bocne veze). Ovo omogucava mrezi da efikasno konstruise piramidu na sa
razlicitim scale faktorima iz jedne slike. Svaki level sa piramide se moze koristiti za
detektovanje objekata u razlitoj razmeri.


Jedan od velikih problema koji se pojavljivao je bila detekcija lica razlitih velicina u
nekotrolisanim uslovima (prirodi, guzvama u gradu). Posto vec poznati koncept piramida
moze restiti probleme detektovanja sa razlicitim scale faktora, sledeca mreza koristi iste
principe. RetinaFace je mreza nesto novijeg porekla i zasnovna je na istim principima na
kojima se zasniva i RetinaNet, ali je namenjena iskljucio detekciji lica.
RetinaFace predstvalja single stage detektor lica. Tvorci ovog modela su uneli nove ili
unapredilivec postojece metode koriscene u ovu svrhu, kao sto su multi-task obucavanje za
istovremenu predikciju sigurnosti, bounding box-a, 5 kljucnih tacaka na licu, i 3D poziciju (u
originalnoj implementaciji).
Ono sto je novo je 5 kljucnih tacaka (keypoint-a) koji ce se kasnije koristiti za poravnanje
lica.



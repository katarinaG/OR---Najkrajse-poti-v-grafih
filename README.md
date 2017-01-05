# OR---Najkrajse-poti-v-grafih

Avtor: Katarina Gačnik, Mateja Smrekar
Projekt pri predmetu Operacijske raziskave 

OPIS PROBLEMA

V najini nalogi se bova ukvarjali z dvema različnima metodama za iskanje najkrajše poti v grafih. Primerjali bova njuni hitrosti na gostih grafih (z velikim številom povezav) in grafih z malo povezavami. Analizo bova naredili tudi na nekaj konkretnih primerih. 

DIJKSTROV ALGORITEM

Prva metoda, katero bomo obravnavale je Dijkstrov algoritem. Ta poišče najkrajšo pot v usmerjenem ali neusmerjenem grafu G(V,E) s pozitivnimi utežmi w. V danem grafu izberemo vozlišče S∈ V(G), ki mu pravimo izvor. Iščemo drevo najkrajših poti od S v G. 

Opis algoritma

Vhodni podatki: G, S
Izhodni podatki: d[ ],π[ ]  (seznam razdalj in prednikov)
for v ∈ V(G):
	π[v] = None
	d[v]= ∞
d[S]=0
Q = V(G)
dokler Q neprazna:
	u = vozlišče iz Q, ki ima najkrajšo d[ ]
	odstranimo u iz Q
	for v ∈ sosed(u):
		if d[v] > d[u] + w(uv):
			d[v] = d[u] + w(uv)
			π[v] = u
return d[ ], π[ ]

Za negativne uteži lahko Dijkstrov algoritem vrne napačen rezultat, če pa so uteži w=0, pa dela pravilno. Večino algoritmov, tudi tega, lahko spremenimo, da delajo pravilno, če odstranimo cikle, ki imajo negativno skupno težo.
Če iščemo razdaljo od S do T, lahko algoritem končamo, ko vzamemo T iz Q.

BELLMAN-FORDOV ALGORITEM

Druga metoda, ki jo bomo uporabile, bo Bellman-Fordov algoritem. Le ta poišče najkrajše poti v usmerjenem in uteženem grafu s poljubnimi utežmi. (Če ima graf samo pozitivne uteži, raje uporabimo Dijkstrov algoritem, ki bo isti problem rešil v krajšem času.)
Predpostavimo, da imamo usmerjen in utežen graf G(V, E) in da graf ne vsebuje negativnega cikla. Označimo število vozlišč: n = |V|. Potem nobena najkrajša pot nima več kot n - 1 povezav. Naredimo prav toliko korakov. Algoritem sloni na dinamičnem programiranju. Po i-tem koraku poznamo najkrajše poti med vozlišči, ki nimajo več kot i povezav. Na koncu še preverimo ali obstaja negativen cikel.

Opis algoritma

Imamo graf G = (V,E), izhodiščno točko v in uteži na povezavah e. Algoritem nam vrne vrednost True, drevo najkrajših poti π, kjer je π[u] prednik vozlišča u, in njihove teže d, kjer je d[u] teža najkrajše poti od v do u, pri pogoju, da ni negativnega cikla dosegljivega iz v. Sicer nam algoritem vrne vrednost False.
Na začetku nastavimo π[u] =  0, d[u] = ∞, d[v]=0 (ker še ni nobene poti od v do vseh ostalih točk). Pogledamo najkrajše poti do najbližnjih točk od v in se prestavimo na naslednjo točko. Zopet pogledamo najkrajše poti do najbližnjih točk razen v. Če je kakšna pot krajša kot je bila pri prejšnjem koraku, jo zamenjamo z novo (krajšo). Ponavljamo, dokler ne pridemo do zadnje točke. Teh korakov je n − 1. Na vsakem koraku se relaksirajo vse povezave grafa natanko enkrat. Na koncu še preverimo, če obstaja negativen cikel.


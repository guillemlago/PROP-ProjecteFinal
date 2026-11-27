<div align="center">

<img src="../img/coet.png" alt="Bombardment" width="120">

<h3>PROP Projecte 26-27/Q2</h3>

<h1>BOMBARDMENT</h1>

<p>Professor: Bernat Orellana<br>CS / EPSEVG</p>

<br>

<img src="../img/logo.png" alt="EPSEVG" width="260">

</div>

---

## Continguts

- [Introducció](#introducció)
- [El joc](#el-joc)
- [Estructura del projecte](#estructura-del-projecte)
- [Posada en marxa](#posada-en-marxa)
- [El vostre jugador](#el-vostre-jugador)
  - [Contracte de temps (important)](#contracte-de-temps-important)
  - [Normes](#normes)
  - [`GameStatus`](#gamestatus)
- [Banc de proves: challenges](#banc-de-proves-challenges)
- [Avaluació](#avaluació)
  - [Resultats contra profe1 (5 punts)](#resultats-contra-profe1-5-punts)
  - [Resultats contra profe2 (2 punts)](#resultats-contra-profe2-2-punts)
  - [Documentació (3 punts)](#documentació-3-punts)
  - [Torneig (bonus, fins a 1 punt extra)](#torneig-bonus-fins-a-1-punt-extra)
- [Registre d'experiments](#registre-dexperiments)
- [Ús de la IA](#ús-de-la-ia)
- [Lliurament](#lliurament)

---
## Introducció

El projecte final de PROP consisteix a programar un jugador automàtic de **Bombardment** (veure regles més endavant) usant l'algorisme **minimax, poda alfa-beta i aprofundiment iteratiu limitat per temps**, i una heurística pròpia.

L'objectiu és portar el vostre jugador al màxim, aplicant totes les optimitzacions que considereu oportunes sobre el minimax+poda de base, tenint en compte millores estàndard (com les taules de transposició, Zobrist, variants de cerca, etc.), així com millores fetes a mida per a aquest joc.

Es proporciona un jugador de referència d'un nivell mig, *profe1*, que us servirà de *sparring* per entrenar el vostre jugador. El jugador amagat, *profe2*, d'un nivell superior serà el repte final que permetrà avaluar si heu dissenyat una bona feina d'enginyeria.

Recordeu que hi haurà també una competició entre tots els vostres bots per aconseguir fins a un punt extra de la nota final de PROP, com es detalla més endavant.

**IMPORTANT**: El projecte és per parelles, que caldrà registrar-vos al [Registre](https://docs.google.com/spreadsheets/d/1K2ne3P7kNAUARL9qk55Bv8w2oZKW5sFfFC0SWEL_uvk/edit?usp=sharing) el més aviat possible, per facilitar el procés a les persones que encara no tenen una persona "reservada".


## El joc

Tauler n x n (per defecte 8x8). Cada jugador comença amb 2 files de pedres: les blanques (PLAYER1) a baix i les negres (PLAYER2) a dalt. Comencen les blanques. A cada torn feu **una** d'aquestes jugades:

- **Pas**: una pedra pròpia avança una fila, recte o en diagonal, a una casella **buida**. No hi ha captures per desplaçament.
- **Explosió**: una pedra pròpia esclata i elimina ella mateixa i **totes** les pedres, de qualsevol color, de les 8 caselles veïnes.

Guanyeu si porteu una pedra a la fila del fons del rival, o si sou els únics que encara teniu pedres. Si una explosió buida el tauler, són taules. Com que totes les jugades avancen o eliminen pedres, les posicions no es repeteixen mai i tota partida acaba.

El joc és de Chris Huntoon (2003). En trobareu la descripció original a [World of Abstract Games: Bombardment](https://jpneto.github.io/world_abstract_games/bombardment.htm).

![Interfície gràfica: profe1 (blanques) contra un jugador aleatori](../img/ui.png)

## Estructura del projecte

```
PROP_Bombardment_alumnes/
├── pom.xml                 superprojecte (agrega els mòduls)
├── bombardment-api/        model del joc i interfícies (GameStatus, Move, IPlayer...) i motor de partides
├── bombardment-player/     EL VOSTRE JUGADOR: és l'únic projecte que lliurareu (amb doc/ i experiments/)
├── bombardment-ui/         interfície gràfica per jugar i veure partides
├── bombardment-bench/      banc de proves: Challenge (moltes partides entre dos jugadors)
├── scripts/                scripts .sh (Linux/macOS) i .bat (Windows) per a la UI i cada banc de proves
├── lib/repo/               jugador del professor de nivell 1 (compilat)
├── challenges/             configuracions de challenges (benchmark oficial 1 i la seva validació)
├── openings/               jocs d'obertures
├── docs/img/               imatges d'aquest README
└── results/                aquí es desen els resultats (HTML + CSV)
```

`bombardment-player` és un projecte Maven **independent**: no hereta del superprojecte, perquè s'ha de poder compilar sol quan el lliureu. Només depèn de `bombardment-api`.

## Posada en marxa

1. Cal JDK 17 o posterior i Maven (NetBeans ja el porta).
2. Des de la carpeta arrel: `mvn install` (o, a NetBeans, *Open Project* sobre la carpeta arrel i *Build* del superprojecte). Això deixa l'API al vostre repositori Maven local.
3. Obriu la interfície gràfica amb `scripts/ui.sh` (Windows: `scripts\ui.bat`) o, a NetBeans, *Run Project* sobre `bombardment-ui`.

Els scripts no fan servir arguments. Cadascun té, al principi, una secció **CONFIGURACIÓ** amb variables (jugadors, temps, mida...) que ja porten els valors de la competició, i línies comentades amb altres valors possibles: editeu-les i executeu l'script. Per defecte, cada script recompila el projecte abans d'executar-se, de manera que sempre agafa la darrera versió del vostre jugador (`BUILD=0` ho evita).

Per jugar contra el vostre jugador, trieu `human` en un costat i la vostra classe a l'altre. Els desplegables són editables: hi podeu escriure qualsevol especificació de jugador (vegeu més avall).

A la UI, cliqueu una pedra pròpia per seleccionar-la: es marquen els destins possibles i, si hi deixeu el ratolí a sobre, la zona d'explosió. Cliqueu un destí per moure-la, o torneu a clicar la mateixa pedra (o feu clic dret) per fer-la esclatar.

**Jugadors aïllats**: amb la casella desmarcada, el jugador corre dins la mateixa JVM i podeu posar punts d'aturada al vostre codi. Marcada, corre en una JVM pròpia, com als challenges i al torneig.

## El vostre jugador

Comenceu per `bombardment-player/src/main/java/edu/upc/epsevg/prop/bombardment/player/MyPlayer.java`.

**No canvieu el nom de la classe `MyPlayer` ni el seu paquet** (`edu.upc.epsevg.prop.bombardment.player`), ni la propietat `player.class` del `pom.xml`: les eines de correcció carreguen exactament aquesta classe. Podeu afegir totes les classes auxiliars que vulgueu. El nom del vostre jugador, el que surt a la UI i als resultats, és el que retorna `getName()`: aquest sí que el podeu canviar.

```java
public interface IPlayer {
    PlayerMove move(GameStatus s);   // retorna la jugada
    void timeout();                  // s'ha acabat el temps: retorneu JA la millor jugada trobada
    String getName();
}
```

### Contracte de temps (important)

Quan s'esgota el temps, el motor crida `timeout()` des d'un altre fil. A partir d'aquí `move()` ha de retornar **immediatament** la jugada de la darrera iteració completada. Si no respon dins el marge de gràcia (**100 ms**; 1 s a les 3 primeres jugades del procés, mentre la JVM encara és freda), **el motor mata el procés del vostre jugador i perdeu la partida**. El mateix passa si llanceu una excepció, retorneu `null` o una jugada il·legal, o el procés mor (p.ex. per `OutOfMemoryError`).

Patró recomanat: un `volatile boolean` que `timeout()` posa a cert i que la cerca consulta a cada node.

### Normes

<img src="../img/warning.svg" alt="Atenció" width="64" align="left">

Incomplir aquestes normes pot fer que el motor mati el vostre jugador o que el lliurament es consideri no vàlid.
<br clear="left">

- La cerca ha de fer servir **un sol fil**. La JVM del jugador es llança amb `-XX:ActiveProcessorCount=1`.
- Memòria: `-Xmx1g`. Dimensioneu la taula de transposicions (si en feu) d'acord amb això.
- Res de fitxers, xarxa, `System.exit` ni pensar durant el torn del rival.
- `System.out` es redirigeix a un fitxer de registre (`results/logs/`). Podeu escriure-hi per depurar, però no abuseu: costa temps.

### `GameStatus`

Coordenades: `x` = columna, `y` = fila. La fila 0 és la de les blanques. Notació: `c2-d3` és un pas, `e5*` una explosió. Els valors de casella són `1` (PLAYER1, blanques), `-1` (PLAYER2, negres) i `0` (buida).

#### Constructors

```java
public GameStatus(int n)
```

Tauler n x n amb 2 files de pedres per jugador. Comencen les blanques.

---

```java
public GameStatus(int n, int rows)
```

Igual, amb `rows` files inicials per jugador.

---

```java
public GameStatus(byte[][] board, PlayerType nextTurnPlayer)
```

Posició arbitrària, útil per a proves. `board[y][x]` amb valors `1`, `-1` o `0`; el tauler ha de ser quadrat. Compte: la primera fila de la matriu (`y = 0`) és la de **baix** (blanques), de manera que al codi el tauler es veu cap per avall.

```java
byte[][] board = {
    { 1,  1,  0,  0,  0},   // y = 0: fila de sortida de les blanques
    { 0,  1,  0,  0,  0},   // y = 1
    { 0,  0, -1,  0,  0},   // y = 2
    { 0,  0,  0,  0,  0},   // y = 3
    {-1, -1,  0,  0, -1},   // y = 4: fila de sortida de les negres
};
GameStatus s = new GameStatus(board, PlayerType.PLAYER1);   // mouen les blanques

s.getPos(2, 2);             // -1: pedra negra a c3
s.explosionBalance(1, 1);   // -2: si b2 esclata, cau 1 negra (c3) i 3 blanques (a1, b1 i ella mateixa)
System.out.print(s);
//  5  B B . . B
//  4  . . . . .
//  3  . . B . .
//  2  . W . . .
//  1  W W . . .
//     a b c d e
```

---

```java
public GameStatus(GameStatus other)
```

Còpia. És la manera senzilla de generar fills.

---

```java
public static GameStatus fromFen(String fen)
```

Crea una posició a partir d'un FEN (vegeu `toFen`).

#### Consultes

```java
public int getSize()
```

Mida n del tauler.

---

```java
public boolean isInside(int x, int y)
```

Cert si (x, y) és dins el tauler.

---

```java
public int getPos(int x, int y)
public int getPos(Point p)
```

Contingut de la casella: `1`, `-1` o `0`.

---

```java
public PlayerType getCurrentPlayer()
```

Jugador que ha de moure.

---

```java
public boolean isGameOver()
```

Cert si la partida ha acabat.

---

```java
public PlayerType getWinner()
```

Guanyador, o `null` si la partida no ha acabat o és taules.

---

```java
public boolean isDraw()
```

Cert si una explosió ha buidat el tauler (taules).

---

```java
public int getStoneCount(PlayerType p)
```

Nombre de pedres del jugador.

---

```java
public List<Point> getStones(PlayerType p)
```

Posicions de les pedres del jugador.

---

```java
public int getGoalRow(PlayerType p)
```

Fila que el jugador ha d'assolir per guanyar.

---

```java
public Move getLastMove()
```

Darrera jugada aplicada, o `null`.

---

```java
public int getPlies()
```

Nombre de jugades (plies) fetes.

---

```java
public String toFen()
```

Posició en text: files de dalt a baix separades per `/`, amb `W`, `B` o `.`, i el torn (` w` o ` b`). Exemple 4x4: `BBBB/..../..../WWWW w`.

---

```java
public boolean equals(Object o)
public int hashCode()
public String toString()
```

Igualtat per tauler i torn. `toString` dibuixa el tauler.

#### Jugades

```java
public List<Move> getMoves()
```

Totes les jugades legals: primer els passos i després les explosions. L'ordre **no** està pensat per a la poda (ordenar és feina vostra). Retorna una llista nova; buida si la partida ha acabat.

---

```java
public boolean isLegal(Move m)
```

Cert si la jugada és legal en aquesta posició.

---

```java
public int explosionBalance(int x, int y)
```

Pedres rivals eliminades menys pedres pròpies (inclosa la que esclata) si esclata la pedra de (x, y). `0` si la casella és buida.

---

```java
public void movePiece(Move m)
```

Aplica la jugada i passa el torn. Llança `IllegalArgumentException` si és il·legal.

#### Herència

```java
protected void setCell(int x, int y, int v)
```

Únic punt on es modifica el tauler. Sobreescriviu-lo si hereteu de `GameStatus` (p. ex. per mantenir un hash Zobrist) i crideu `super.setCell(...)`. Els constructors no el criden.

`forceLoser(PlayerType p)` també és públic, però només el fa servir el motor (temps esgotat o jugada il·legal): no el crideu.

## Banc de proves: challenges

És al projecte `bombardment-bench` (`bench.Challenge`) i s'executa amb `scripts/challenge.sh` (Windows: `scripts\challenge.bat`). També podeu fer *Run File* a NetBeans sobre la classe.

Moltes partides entre dos jugadors qualssevol. Cada obertura es juga dues vegades canviant els colors. Cada challenge és un fitxer `.properties` de `challenges/` (jugadors, mida, temps, obertures, paral·lelisme): per fer-ne un, copieu `exemple.properties` i editeu-lo. A `scripts/challenge.sh` trieu quin fitxer s'executa amb la variable `CONFIG` (per defecte, `challenges/exemple.properties`).

Jugadors possibles (`playerA` / `playerB`):

| Especificació | Jugador |
|---|---|
| `random` | aleatori |
| `profe1` | professor, nivell 1 (heurística simple) |
| `edu.upc.epsevg.prop.bombardment.player.MyPlayer` | la vostra classe |
| `edu.upc.epsevg.prop.bombardment.player.MyPlayer(4,true)` | amb arguments per al constructor (String, int, long, double, boolean) |
| `v2=edu.upc.epsevg.prop.bombardment.player.MyPlayer(2)` | amb una etiqueta curta per als informes |
| `jar:ruta/jugador.jar` | un jugador empaquetat (`mvn package` del vostre projecte) |

Així podeu comparar versions de la vostra heurística entre elles (`playerA=v1=edu.upc.epsevg.prop.bombardment.player.MyPlayer(1)`, `playerB=v2=edu.upc.epsevg.prop.bombardment.player.MyPlayer(2)`). Els resultats es desen a `results/` (un resum en HTML, que podeu obrir amb el navegador, i un CSV amb totes les partides): puntuació, error estàndard, diferència Elo, profunditat mitjana i incidències.

**Comproveu sempre les incidències.** El resum les mostra destacades: partides perdudes per no respondre a temps (el procés ha estat mort), per excepcions, per jugades il·legals o perquè el procés ha mort. Una sola incidència vol dir que el vostre jugador no respecta el contracte de temps o té un error, i a la correcció cada incidència és una partida perduda. Al resum també hi ha el temps màxim de resposta: si s'acosta a 200 + 100 ms, aneu just.

Jocs d'obertures 8x8 a `openings/`: `prova-10`, `prova-25` i `prova-50` per a proves ràpides (20, 50 i 100 partides; uns 3, 8 i 15 minuts a 200 ms), `benchmark-A` (100 obertures, 200 partides, prop d'una hora) per al benchmark 1, i `benchmark-B` (100 obertures més) per a validació. Cap d'aquests jocs comparteix obertures amb els altres.

**Validació contra el sobreajustament.** Si ajusteu l'heurística mirant només `benchmark-A`, pot ser que acabi ajustada a aquelles obertures concretes. Per comprovar-ho, executeu `challenges/benchmark-validacio-1-profe1.properties`: és la mateixa configuració que el benchmark 1, però amb les obertures de `benchmark-B`. No compta per a la nota. Si el resultat amb B és clarament pitjor que amb A (més de 2 errors estàndard, uns 7 punts amb 200 partides), hi ha sobreajustament. Feu servir B només per validar, no per ajustar: si també hi ajusteu, deixa de servir per detectar-lo.

Interpretació: amb 200 partides, l'error estàndard és d'uns ±3,5 punts. Una diferència de 2 o 3 punts entre dues versions **no** és significativa. Per comparar heurístiques feu servir moltes partides i més d'un joc d'obertures.

## Avaluació

La nota de la pràctica (sobre 10) té tres parts. Les dues primeres depenen de la **puntuació** que obtingueu en un challenge de N partides:

$$\text{Puntuació} = \frac{V + E/2}{N} \times 100\%$$

on V és el nombre de victòries, E el nombre d'empats (taules) i N el total de partides jugades. Cada victòria val 1, cada empat 0,5 i cada derrota 0. Les partides perdudes per incidències (temps, excepcions, jugades il·legals) compten com a derrotes.

Dins de cada tram de les taules següents, els punts s'interpolen linealment. Si la puntuació P cau al tram que va de P₀ (on es donen a punts) a P₁ (on es donen b punts):

$$\text{Punts} = a + \frac{P - P_0}{P_1 - P_0} \cdot (b - a)$$

Exemple contra profe1: 200 partides amb 80 victòries, 10 empats i 110 derrotes donen (80 + 5) / 200 = 42,5%. Això cau al tram de 30% a 75% (de 2,5 a 5 punts): 2,5 + (42,5 − 30) / (75 − 30) × 2,5 ≈ **3,19 punts**.

### Resultats contra profe1 (5 punts)

200 partides (100 obertures × 2 colors) a 200 ms per jugada, amb la configuració de `challenges/benchmark-1-profe1.properties`.

**Atenció:** per a la correcció, el joc d'obertures es pot canviar per un altre de la mateixa mida. No ajusteu el jugador només per a les obertures de `benchmark-A`: feu servir també els jocs `prova-*` i valideu-lo amb `benchmark-B` (vegeu [Banc de proves](#banc-de-proves-challenges)).

| Puntuació | Punts |
|---|---|
| jugador no funcional | 0 |
| de 0% a 10% | de 0 a 1 (lineal) |
| de 10% a 30% | de 1 a 2,5 (lineal) |
| de 30% a 75% | de 2,5 a 5 (lineal) |
| 75% o més | 5 |

### Resultats contra profe2 (2 punts)

200 partides a 200 ms per jugada contra un jugador del professor de nivell 2, amb un altre joc d'obertures (que tampoc es publica). Aquest jugador no es distribueix: els resultats es publicaran amb el torneig.

| Puntuació | Punts |
|---|---|
| menys del 5% | 0 |
| de 5% a 30% | de 0 a 1,5 (lineal) |
| de 30% a 70% | de 1,5 a 2 (lineal) |
| 70% o més | 2 |

### Documentació (3 punts)

Tota la documentació va dins la carpeta `doc/` del vostre projecte (`bombardment-player/doc/`). La memòria s'escriu en **Markdown** (`doc/memoria.md`); les taules i els gràfics s'hi incorporen com a imatges, desades a `doc/img/` i enllaçades amb rutes relatives (`![Profunditat per versió](img/profunditat.png)`).

- **1,25 punts · Millores i optimitzacions.** Explicació detallada de les millores i optimitzacions aplicades a la cerca, amb una comparativa del rendiment amb i sense cadascuna (challenges entre versions del vostre jugador).
- **1,25 punts · Heurística.** Explicació detallada i discussió de l'heurística: per què funciona, quins experiments heu fet per ajustar-ne els paràmetres i com justifiqueu que cada part aporta valor.
- **0,5 punts · Resum de resultats.**
- **Declaració d'ús de la IA (obligatòria).** Secció final de la memòria; vegeu l'apartat [Ús de la IA](#ús-de-la-ia).
- **Registre històric de proves (obligatori).** Vegeu l'apartat següent. **Si no hi és o no és coherent, pot invalidar tot el lliurament.**

### Torneig (bonus, fins a 1 punt extra)

Després del lliurament es farà un torneig entre tots els equips. Dona punts extra, fora de la nota anterior:

| Posició | Bonus |
|---|---|
| Guanyador | +1 |
| Finalista | +0,5 |
| 3r i 4t | +0,25 |

## Registre d'experiments

Durant tot el projecte heu de mantenir el fitxer `doc/registre.md`: un registre per dates de l'evolució del projecte, què heu fet a cada etapa, quines proves heu fet i amb quin resultat.

1. **Repositori.** Treballeu en un repositori de GitHub **privat** i afegiu-hi el professor com a col·laborador.
2. **Tags.** Cada etapa del registre correspon a un tag de GitHub (per exemple `v0.4-killers`). Si es fa `git checkout` d'aquell tag, s'hi ha de trobar el codi que es va provar.
3. **Proves.** Cada etapa explica breument les proves fetes (rivals, nombre de partides, obertures, temps per jugada) i els resultats (puntuació ± error, profunditat, incidències).
4. **Fitxers.** Copieu el resum `.html` i el `.csv` de cada challenge que citeu, des de `results/` a `bombardment-player/experiments/`, i feu-ne commit al mateix tag. El número que poseu al registre ha de sortir d'aquests fitxers.

Exemple d'entrada:

> **2026-12-12 · tag `v0.4-killers`**: afegim killer moves. Challenge `v0.4` vs `v0.3`, 200 partides amb `prova-50` a 200 ms → 58,5% ± 3,4; profunditat mitjana de 6,1 a 6,6; cap incidència. Fitxers: `experiments/2026-12-12-killers.html` i `.csv`.

`doc/registre.md` ja conté una plantilla.

## Ús de la IA

Podeu fer servir eines d'IA com a **suport**, però el codi i l'anàlisi els heu d'escriure vosaltres. El criteri és aquest:

| | Ús | Exemples |
|---|---|---|
| 🟢 | **Lliure** | Consultar dubtes de Java o de l'algorisme, ajuda per depurar errors, scripts d'automatització de proves, gràfiques i taules a partir dels CSV, revisió de la redacció. |
| 🟡 | **Permès, però cal declarar-lo** | Autocompletat (*code completion*) i suggeriments de fragments petits dins el jugador, refactoritzacions. |
| 🔴 | **No permès** | Demanar a la IA el jugador, la cerca o l'heurística sencers (p. ex., enganxant-li aquest README), o que escrigui l'anàlisi i les conclusions de la memòria. |

Tot ús 🟡 s'ha de declarar a la secció **Declaració d'ús de la IA** de la memòria (`doc/memoria.md`): quina eina, per a què i alguns exemples de les peticions que hi heu fet. Fer servir la IA sense declarar-ho es considera una falta.

> [!IMPORTANT]
> **A la prova final es faran exercicis de validació** que poden incloure **ampliacions del codi del vostre projecte** i **preguntes teòriques que assumeixen un coneixement profund del problema**. Si no enteneu i no sou capaços de modificar el codi que heu lliurat, no les podreu resoldre.

## Lliurament

Només cal que lliuri un dels integrants del grup. Heu de presentar un únic zip que contingui **la carpeta `bombardment-player`** sencera (codi, `pom.xml`, `doc/` i `experiments/`), **sense** `target/`. És a dir, en obrir el zip s'ha de veure la carpeta, no els fitxers solts:

```
G_E76.zip
└── bombardment-player/
    ├── pom.xml
    ├── src/
    ├── doc/
    └── experiments/
```

Des de l'arrel del superprojecte (canvieu `G_E76` pel vostre `ID_EQUIP`):

Linux / macOS (sh):

```sh
cd bombardment-player && mvn clean && cd ..
zip -r G_E76.zip bombardment-player -x "*/.git/*" "*/target/*"
```

Windows (cmd):

```bat
cd bombardment-player && mvn clean && cd ..
tar -a -c -f G_E76.zip --exclude=.git --exclude=target bombardment-player
```

`tar -a` amb extensió `.zip` genera un zip normal; ve amb Windows 10 i posteriors. També podeu fer clic dret sobre la carpeta `bombardment-player` i *Envia a > Carpeta comprimida*, després de `mvn clean`, i reanomenar el zip.

**Nom del zip.** El nom de l'arxiu zip correspon al nom de l'equip tal com està registrat al document compartit "Equips del Projecte". La inscripció és obligatòria, i cal indicar-hi necessàriament els NIF dels membres.

```
[ID_EQUIP].zip
```

Cada fila del document de registre té assignat un `ID_EQUIP`. Per exemple, l'equip KingAfrica, amb `ID_EQUIP` G_E76, lliurarà un arxiu anomenat `G_E76.zip`.

Abans de lliurar, comproveu que el projecte compila sol: descomprimiu el zip en una carpeta nova, fora del superprojecte, i feu-hi `mvn package`.

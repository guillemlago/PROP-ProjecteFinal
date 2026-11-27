# Java: colecciones y mapas

Fuente local: `Java (2).pdf`. Ámbito: Java y programación orientada a objetos.

Transcripción del texto disponible en el PDF, en su idioma original y por páginas. Los bloques de texto conservan ejemplos, símbolos y disposición sin reinterpretarlos. La vista original de cada página conserva diagramas, tablas, capturas y texto integrado en imágenes. La extracción automática puede contener errores de orden o caracteres; contrastar los detalles con esa vista.

[Índice de documentación](README.md)

## Página 1

```text
PROP    2022-2023    Q2
                                                Mario Martin – Ignasi Gómez Sebastià – Bernat Orellana
```

<details>
<summary>Ver página original</summary>

![Página 1 de Java: colecciones y mapas](img/java-colecciones/pagina-001.webp)

</details>

## Página 2

```text
Ja   hem      vist   els   següents          conceptes          de   POO
       -

           -  Sobrecàrrega          (Overloading)


           -  Overriding


           -  Polymorphism


          Una      bona      forma       de   veurel’s       son    les
       -

          col·leccions          i mapes












      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            2
```

<details>
<summary>Ver página original</summary>

![Página 2 de Java: colecciones y mapas](img/java-colecciones/pagina-002.webp)

</details>

## Página 3

```text
-   El llenguatge       Java   proporciona        implementacions           per   moltes

         estructures      de   dades


     -   Es  defineix     una   "col·lecció"     com    "un   objecte    que   representa

         un  grup   d'objectes".


     -   És  "una    arquitectura      unificada      per  representar       i manipular

         col·leccions,      el que   els  permet      ser  manipulat

         independentment            dels   detalls    de  la seva    representació".


     -   Totes    a Java.util:

         import      java.util.*;

         o


         import      java.util.Collection;



      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            3
```

<details>
<summary>Ver página original</summary>

![Página 3 de Java: colecciones y mapas](img/java-colecciones/pagina-003.webp)

</details>

## Página 4

```text
Les    col·leccions          són     classes      genèriques,           és   a
       -

          dir,   col·leccions          de   objectes         de   qualsevol


          classe.


          Exemples:
       -

           -  ArrayList<Node>


           -  LinkedList<String>












      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            4
```

<details>
<summary>Ver página original</summary>

![Página 4 de Java: colecciones y mapas](img/java-colecciones/pagina-004.webp)

</details>

## Página 5

```text
public    class    GenericClass<T>         {

           private     T  obj;

           public     void   setObj(T      t)  {obj   =  t;}

           public     T  getObj()     {return     obj;}

           public     void   print()     {

                 System.out.println(obj);

           }

       }










      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            5
```

<details>
<summary>Ver página original</summary>

![Página 5 de Java: colecciones y mapas](img/java-colecciones/pagina-005.webp)

</details>

## Página 6

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            6
```

<details>
<summary>Ver página original</summary>

![Página 6 de Java: colecciones y mapas](img/java-colecciones/pagina-006.webp)

</details>

## Página 7

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            7
```

<details>
<summary>Ver página original</summary>

![Página 7 de Java: colecciones y mapas](img/java-colecciones/pagina-007.webp)

</details>

## Página 8

```text
Una      List   pot    utilitzar      dos    sistemes         diferents
       -

          per    ser    emmagatzemada:







            Com  un array

             (ArrayList)








      Com  una llista doblement

              enllaçada
             (LinkedList)


      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            8
```

<details>
<summary>Ver página original</summary>

![Página 8 de Java: colecciones y mapas](img/java-colecciones/pagina-008.webp)

</details>

## Página 9

```text
Un     Set   pot    utilitzar      dos     sistemes         diferents        per
       -

          ser    emmagatzemat:



                                                          https://www.thecshandbook.com/hash_set














          Arbre balancejat Red-Black

                   (TreeSet)
                                                                       Taula hash
                                                                        (HashSet)

      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            9
```

<details>
<summary>Ver página original</summary>

![Página 9 de Java: colecciones y mapas](img/java-colecciones/pagina-009.webp)

</details>

## Página 10

```text
https://www.thecshandbook.com/hash_set















     Com   busca Java un element  al HashSet/HashMap?    Usant  les funcions hashCode()  i equals()
     de la classe afectada.



                              hashCode(88)   8
                              Accedim a la posició 8 i si hi ha més d’un ítem, busquem el 88
                   88 ?
                              88 equals(538) ?  false
                              88 equals(88) ?  true



      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            10
```

<details>
<summary>Ver página original</summary>

![Página 10 de Java: colecciones y mapas](img/java-colecciones/pagina-010.webp)

</details>

## Página 11

```text
Classe      Thread safe Iteració    Accés indexat Cerca de valor Inserció TAD


                                       Ordre                   Lineal (O(n)),
                 ArrayList NO                      O(1)                     O(n)        Array dinàmic
                                       d’inserció              equals()

                                       Ordre                   Lineal (O(n)),           Array dinàmic
                                                   O(1)                     O(n)
                 Vector    SI          d’inserció              equals()
   List

                                       Ordre                   Lineal (O(n)), Cost de   Llista
                LinkedList NO          d’inserció  O(n)        equals()     cerca(si cal) + doblement
                                                                            O(1)        enllaçada

                                       Ordre natural (
                                                               Binària
                                       requereix                            O(log(n)) (en Arbre binari
                 TreeSet   NO                      N/D         O(log(n)),
                                       Comparable o                         mitja)      balancejat
                                                               compareTo
                                       Comparator)
   Set
                                                                                        Taula hash
                                                               Constant.O(k)
                                                                                        amb col·lisions
                                                               hashCode() +
                 HashSet   NO          No hi ha ordre N/D                   O(k)        gestionada
                                                               equals() per
                                                                                        amb separate
                                                               les col·lisions
                                                                                        chaining
      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            11
```

<details>
<summary>Ver página original</summary>

![Página 11 de Java: colecciones y mapas](img/java-colecciones/pagina-011.webp)

</details>

## Página 12

```text
Mètodes   de  la interfície




























      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            12
```

<details>
<summary>Ver página original</summary>

![Página 12 de Java: colecciones y mapas](img/java-colecciones/pagina-012.webp)

</details>

## Página 13

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            13
```

<details>
<summary>Ver página original</summary>

![Página 13 de Java: colecciones y mapas](img/java-colecciones/pagina-013.webp)

</details>

## Página 14

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            14
```

<details>
<summary>Ver página original</summary>

![Página 14 de Java: colecciones y mapas](img/java-colecciones/pagina-014.webp)

</details>

## Página 15

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            15
```

<details>
<summary>Ver página original</summary>

![Página 15 de Java: colecciones y mapas](img/java-colecciones/pagina-015.webp)

</details>

## Página 16

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            16
```

<details>
<summary>Ver página original</summary>

![Página 16 de Java: colecciones y mapas](img/java-colecciones/pagina-016.webp)

</details>

## Página 17

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            17
```

<details>
<summary>Ver página original</summary>

![Página 17 de Java: colecciones y mapas](img/java-colecciones/pagina-017.webp)

</details>

## Página 18

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            18
```

<details>
<summary>Ver página original</summary>

![Página 18 de Java: colecciones y mapas](img/java-colecciones/pagina-018.webp)

</details>

## Página 19

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            19
```

<details>
<summary>Ver página original</summary>

![Página 19 de Java: colecciones y mapas](img/java-colecciones/pagina-019.webp)

</details>

## Página 20

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           20
```

<details>
<summary>Ver página original</summary>

![Página 20 de Java: colecciones y mapas](img/java-colecciones/pagina-020.webp)

</details>

## Página 21

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            21
```

<details>
<summary>Ver página original</summary>

![Página 21 de Java: colecciones y mapas](img/java-colecciones/pagina-021.webp)

</details>

## Página 22

```text
Una  implementació     de les col·leccions




























      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           22
```

<details>
<summary>Ver página original</summary>

![Página 22 de Java: colecciones y mapas](img/java-colecciones/pagina-022.webp)

</details>

## Página 23

```text
Les    classes       que    implementen               la  interfície
     -

         Set<T>           no    permeten           que     un    element          de   la


         classe      aparegui          més      d'una      vegada


         Els   elements          es   comparen           fent    servir     el  métode
     -

         equals

         [Compte          amb      afegir     en    un   conjunt        objectes
     -

         mutables          (poden        canviar).       Si  canvien        es   poden


         violar     les   condicions          de   conjunt]








      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            23
```

<details>
<summary>Ver página original</summary>

![Página 23 de Java: colecciones y mapas](img/java-colecciones/pagina-023.webp)

</details>

## Página 24

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           24
```

<details>
<summary>Ver página original</summary>

![Página 24 de Java: colecciones y mapas](img/java-colecciones/pagina-024.webp)

</details>

## Página 25

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            25
```

<details>
<summary>Ver página original</summary>

![Página 25 de Java: colecciones y mapas](img/java-colecciones/pagina-025.webp)

</details>

## Página 26

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           26
```

<details>
<summary>Ver página original</summary>

![Página 26 de Java: colecciones y mapas](img/java-colecciones/pagina-026.webp)

</details>

## Página 27

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            27
```

<details>
<summary>Ver página original</summary>

![Página 27 de Java: colecciones y mapas](img/java-colecciones/pagina-027.webp)

</details>

## Página 28

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           28
```

<details>
<summary>Ver página original</summary>

![Página 28 de Java: colecciones y mapas](img/java-colecciones/pagina-028.webp)

</details>

## Página 29

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           29
```

<details>
<summary>Ver página original</summary>

![Página 29 de Java: colecciones y mapas](img/java-colecciones/pagina-029.webp)

</details>

## Página 30

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            30
```

<details>
<summary>Ver página original</summary>

![Página 30 de Java: colecciones y mapas](img/java-colecciones/pagina-030.webp)

</details>

## Página 31

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            31
```

<details>
<summary>Ver página original</summary>

![Página 31 de Java: colecciones y mapas](img/java-colecciones/pagina-031.webp)

</details>

## Página 32

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            32
```

<details>
<summary>Ver página original</summary>

![Página 32 de Java: colecciones y mapas](img/java-colecciones/pagina-032.webp)

</details>

## Página 33

```text
Diverses         implementacions                 de    la  interfície
       -
          Set<T>:



           -  TreeSet<T>:                Implementació            com     a arbre


              binari   balancejat.


           -  HashSet<T>:                [Més     usat]   Implementació            amb

              taules    de   Hash



          Exemple:
       -


                Set      s1    =   new      HashSet<Integer>();

                Set      s2    =   new      TreeSet();



      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            33
```

<details>
<summary>Ver página original</summary>

![Página 33 de Java: colecciones y mapas](img/java-colecciones/pagina-033.webp)

</details>

## Página 34

```text
Set   set    =  new   HashSet();      //   instantiate       a  concrete      set

       //   ...

       set.add(obj);         //  insert     an  elements

       //   ...

       int   n   =  set.size();       //  get   size

       //   ...

       if   (set.contains(obj))           {...}    //   check    membership


       //   iterate     through     the   set

       Iterator      iter    =  set.iterator();

       while     (iter.hasNext())         {

          Object     e  =  iter.next();

          //   downcast      e
          //   ...

       }



      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            34
```

<details>
<summary>Ver página original</summary>

![Página 34 de Java: colecciones y mapas](img/java-colecciones/pagina-034.webp)

</details>

## Página 35

```text
-  Les col·leccions només  poden  contenir objectes.

           -  No es pot posar un tipus de dades fonamental   en una col·lecció

       -  Java ha definit "embolcalls" (wrappers)  per a les classes fonamentals que tenen

          només   valors de un tipus fonamental dins de l’objecte


       -  Aquestes  classes es defineixen en java.lang

       -  Cada  tipus de dades fonamental   està representada  per una classe contenidora

          (wrapper). Les classes wrapper  són:

           -    Boolean
           -   Byte

           -   Character
           -   Double
           -   Float

           -   Short
           -   Integer

           -   Long


      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            35
```

<details>
<summary>Ver página original</summary>

![Página 35 de Java: colecciones y mapas](img/java-colecciones/pagina-035.webp)

</details>

## Página 36

```text
-  Crear una classe Llibre amb
           -  ISBN

           -  Títol
       -  Crear una classe Llibreria com a gestora d’un Set de llibres.

           -  Trieu la classe d’implementació del Set adequada, tenint en compte que necessitem mantenir els elements
              ordenats per ordre alfabètic de títol.

           -  Creeu un atribut llibres de la classe que hagueu triat en el punt anterior.
           -  Constructor que crea llibreria buida, inicialitza llibres.

           -  Programeu equals() i hashCode()
           -  Programen toString() , ha de tornar una cadena que sigui un llistat de tots els llibres de la llibreria.

           -  Funció per afegir un llibre a la llibreria. Retorna false si el llibre ja existeix (ISBN repetit!) i per tant no es pot
              afegir. Retorna true si s’ha pogut afegir.

           -  Funció per cercar un llibre a partir d’un fragment del títol. Retorna null si no el troba.
           -  Funció per cercar un llibre a partir de l’ISBN. Ens cal màxima velocitat, i per tant usarem un índex per

              accedir a temps constant. Retorna null si no el troba.
           -  Funció per eliminar un llibre de la llibreria, donat un ISBN. Retorna true si s’ha pogut esborrar el llibre, false
              si no s’ha trobat.

       -  Crear els testos de la classe Llibre.


      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            36
```

<details>
<summary>Ver página original</summary>

![Página 36 de Java: colecciones y mapas](img/java-colecciones/pagina-036.webp)

</details>

## Página 37

```text
Una  implementació     de les col·leccions




























      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            37
```

<details>
<summary>Ver página original</summary>

![Página 37 de Java: colecciones y mapas](img/java-colecciones/pagina-037.webp)

</details>

## Página 38

```text
-   Les   classes    que   implementen         la  interfície    List<T>         tenen


         els  seus   elements      ordenats

     -   Els  elements      s'indexen      començant        per   zero


     -   Una    classe   que   implementa         la interfície    List<T>         permet

         que   els  elements      apareguin       més    d'una    vegada

     -   La  interfície    List<T>         té  més    funcions     que   els  mètodes       de


         la interfície    Collection<T>

     -   Alguns     dels   mètodes      heretats     de   la interfície

         Collection<T>                tenen    semàntiques         diferents    en   la


         interfície    List<T>






      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            38
```

<details>
<summary>Ver página original</summary>

![Página 38 de Java: colecciones y mapas](img/java-colecciones/pagina-038.webp)

</details>

## Página 39

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            39
```

<details>
<summary>Ver página original</summary>

![Página 39 de Java: colecciones y mapas](img/java-colecciones/pagina-039.webp)

</details>

## Página 40

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           40
```

<details>
<summary>Ver página original</summary>

![Página 40 de Java: colecciones y mapas](img/java-colecciones/pagina-040.webp)

</details>

## Página 41

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            41
```

<details>
<summary>Ver página original</summary>

![Página 41 de Java: colecciones y mapas](img/java-colecciones/pagina-041.webp)

</details>

## Página 42

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           42
```

<details>
<summary>Ver página original</summary>

![Página 42 de Java: colecciones y mapas](img/java-colecciones/pagina-042.webp)

</details>

## Página 43

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            43
```

<details>
<summary>Ver página original</summary>

![Página 43 de Java: colecciones y mapas](img/java-colecciones/pagina-043.webp)

</details>

## Página 44

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           44
```

<details>
<summary>Ver página original</summary>

![Página 44 de Java: colecciones y mapas](img/java-colecciones/pagina-044.webp)

</details>

## Página 45

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           45
```

<details>
<summary>Ver página original</summary>

![Página 45 de Java: colecciones y mapas](img/java-colecciones/pagina-045.webp)

</details>

## Página 46

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           46
```

<details>
<summary>Ver página original</summary>

![Página 46 de Java: colecciones y mapas](img/java-colecciones/pagina-046.webp)

</details>

## Página 47

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            47
```

<details>
<summary>Ver página original</summary>

![Página 47 de Java: colecciones y mapas](img/java-colecciones/pagina-047.webp)

</details>

## Página 48

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           48
```

<details>
<summary>Ver página original</summary>

![Página 48 de Java: colecciones y mapas](img/java-colecciones/pagina-048.webp)

</details>

## Página 49

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           49
```

<details>
<summary>Ver página original</summary>

![Página 49 de Java: colecciones y mapas](img/java-colecciones/pagina-049.webp)

</details>

## Página 50

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            50
```

<details>
<summary>Ver página original</summary>

![Página 50 de Java: colecciones y mapas](img/java-colecciones/pagina-050.webp)

</details>

## Página 51

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            51
```

<details>
<summary>Ver página original</summary>

![Página 51 de Java: colecciones y mapas](img/java-colecciones/pagina-051.webp)

</details>

## Página 52

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           52
```

<details>
<summary>Ver página original</summary>

![Página 52 de Java: colecciones y mapas](img/java-colecciones/pagina-052.webp)

</details>

## Página 53

```text
Diverses         implementacions                 de    la  interfície
       -
          List<T>:



           -  ArrayList<T>:                   Implementació            de  la  llista


              amb    una    taula    redimensionable.            Accés     més     rapid.


           -  LinkedList<T>:                    Implementació            de   la llista

              amb    punters.      Insercions       i eliminacions         més


              ràpides



          Exemple:
       -

                List<String>        noms   = new  LinkedList<String>;



      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            53
```

<details>
<summary>Ver página original</summary>

![Página 53 de Java: colecciones y mapas](img/java-colecciones/pagina-053.webp)

</details>

## Página 54

```text
-  Crear   una  classe  que  implementi     una   cua  a partir d’una   ArrayList

           -  Crear    cua   buida

           -  Afegir    element     (a   la  cua,    enqueue)

           -  Preguntar      qui   és  el   primer    de   la   cua.

              ▪ Retorneu    null   si la  cua  es  buida
           -  “Servir”     el   primer    de   la  cua    (l’eliminem,       dequeue)



       -  Crear   una  classe  que  implementi     una   pila a partir d’una   LinkedList

           -  Crear    pila   buida
           -  Afegir    element     a  la   pila   (Apilar      o  push)

           -  Preguntar      quin   element     hi   ha   a  dalt   de   la  pila

              ▪ Retorneu    null   si la  cua  es  buida

           -  Desapilar      l’element      més   a  dalt    de  la   pila   (pop)






      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           54
```

<details>
<summary>Ver página original</summary>

![Página 54 de Java: colecciones y mapas](img/java-colecciones/pagina-054.webp)

</details>

## Página 55

```text
Una  agrupació   d’objectes  que  no és una  col·lecció




























      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            55
```

<details>
<summary>Ver página original</summary>

![Página 55 de Java: colecciones y mapas](img/java-colecciones/pagina-055.webp)

</details>

## Página 56

```text
Implementació                de   memòria           associativa
       -

          Parelles        <clau,valor>
       -

          S’obté       el  valor     associat       a  una     clau    no    pel   índex
       -
          sinó     per    un   càlcul     (de    hash)      sobre      la  clau.


          Per    exemple.          Volem       guardar        freqüències           de
       -

          paraules


           -  <String,      Integer>


           -  Accedim       a  nombre       de   vegades       que    apareix     la

              paraula     per   la  mateixa      paraula      (no   per   un   índex

              com    en   una    taula)




      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           56
```

<details>
<summary>Ver página original</summary>

![Página 56 de Java: colecciones y mapas](img/java-colecciones/pagina-056.webp)

</details>

## Página 57

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            57
```

<details>
<summary>Ver página original</summary>

![Página 57 de Java: colecciones y mapas](img/java-colecciones/pagina-057.webp)

</details>

## Página 58

```text
-   Clear()                           Elimina      totes    les  associacions

   -   containsKey(k)                    Si  conté     una    assoc.    per   a  k

   -   containsValue(v)                  Si  conté     una    assoc.    per   a  v

   -   get(k)                            Valor     associat     amb     k

   -   isEmpty()                         Si  esta    buit

   -   keySet()                          Conjunt       de   claus

   -   put(k,v)                           Associar      v  amb     k


   -   remove(k)                         Eliminar       associacions        per   a  k

   -   size()                            Nombre        de   parelles

   -   values()                          Col·lecció       de  valors






      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           58
```

<details>
<summary>Ver página original</summary>

![Página 58 de Java: colecciones y mapas](img/java-colecciones/pagina-058.webp)

</details>

## Página 59

```text
Diverses         implementacions                 de    la  interfície
       -
          Map<K,V>:



           -  HashMap           :    Implementació            del  Map     amb     taules


              de  hast.    [Més    usat]


           -  TreeMap           :Implementació             del   Map     amb     arbres


              balancejats.       Manté       un  ordre.


          Exemple:
       -


    Map<String,Integer>              noms     =  new    HashMap<String,Integer>;

    Map   map    =  new    HashMap();



      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           59
```

<details>
<summary>Ver página original</summary>

![Página 59 de Java: colecciones y mapas](img/java-colecciones/pagina-059.webp)

</details>

## Página 60

```text
Map  map   =  new  HashMap();     //  instantiate     a  concrete    map

       //  ...
       map.put(key,      val);   //  insert   a  key-value     pair

       //  ...

       //  get  the   value   associated     with   key
       Object   val   =  map.get(key);

       map.remove(key);       //  remove    a key-value     pair

       //  ...
       if  (map.containsValue(val))          {  ...  }

       if  (map.containsKey(kay))         {  ...   }

       Set  keys   =  map.keySet();      //  get   the  set  of  keys
       //  iterate    through    the  set   of  keys

       Iterator    iter   =  keys.iterator();

       while   (iter.hasNext())       {
          Key  key   = (Key)   iter.next();

          //  ...

       }
      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           60
```

<details>
<summary>Ver página original</summary>

![Página 60 de Java: colecciones y mapas](img/java-colecciones/pagina-060.webp)

</details>

## Página 61

```text
HashMap<String,         Integer>      frequency(String[]          names)     {



           HashMap<String,         Integer>      frequency      =

                             new   HashMap<String,         Integer>();


           for(String      name    :  names)     {

                 Integer     currentCount        =  frequency.get(name);

                 if(currentCount         ==   null)    {

                       currentCount        =  0;  }

                 frequency.put(name,           ++currentCount);

           }
           return    frequency;

     }





                                                                                              61
```

<details>
<summary>Ver página original</summary>

![Página 61 de Java: colecciones y mapas](img/java-colecciones/pagina-061.webp)

</details>

## Página 62

```text
Per    poder      fer  servir    el  Map,      la  classe     que    es  fa
       -

          servir     com     a  clau   ha   de    tenir   implementats             de   els

          mètodes:




          equals


          hashCode




          En    les  classes      habituals       estan      implementades,
       -

          en   les   pròpies      s’han     de   implementar






      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           62
```

<details>
<summary>Ver página original</summary>

![Página 62 de Java: colecciones y mapas](img/java-colecciones/pagina-062.webp)

</details>

## Página 63

```text
public    class   Person   {
        public   String    name;

        boolean    equals(Object      o)  {
             return    (o  instanceof     Person   &&  ((Person)o).name.equals(name));

        }

        public   int   hashCode()     {
             return    name.hashCode();

        }

  }










                                                                                              63
```

<details>
<summary>Ver página original</summary>

![Página 63 de Java: colecciones y mapas](img/java-colecciones/pagina-063.webp)

</details>

## Página 64

```text
-  Fer   un  programa       que   llegeix   un  text  per   el canal   d’entrada

          estàndard      i mostra     per  pantalla    la freqüència      de  cada

          paraula     diferent    del  text

       -  Mapes     i llistes  amb    futbol:

           -  Crear  classe  futbolista   amb   els camps:

              ▪ Dorsal

              ▪ Nom
              ▪ Gols

           -  Crear  varis futbolistes   i posar-los   a una  llista.

           -  Crear  un  mapa   que   tingui  com   a clau el nombre     de gols,  i com  a

              valor una   llista de futbolistes   que  hagin   marcat   aquest   nombre

              de gols.

           -  Recorreu   la llista de futbolistes   i ompliu   el mapa.

           -  Verifiqueu   que  el contingut    del mapa    és correcte.



      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           64
```

<details>
<summary>Ver página original</summary>

![Página 64 de Java: colecciones y mapas](img/java-colecciones/pagina-064.webp)

</details>

## Página 65

```text
Recorrent  les col·leccions




























      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           65
```

<details>
<summary>Ver página original</summary>

![Página 65 de Java: colecciones y mapas](img/java-colecciones/pagina-065.webp)

</details>

## Página 66

```text
Les    col·leccions          i els   Maps       són    extensions           de
       -

          la  classe      iterables.





          A   la  classe      hi  ha   mètodes          definits       per    recórrer
       -

          els   elements          que     componen            l’objecte       de    la


          classe












      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           66
```

<details>
<summary>Ver página original</summary>

![Página 66 de Java: colecciones y mapas](img/java-colecciones/pagina-066.webp)

</details>

## Página 67

```text
-   Mètodes       implementats


            boolean     hasNext(      );
            Object     next(    );

            void    remove(     );



      -   Mètodes       implementats            addicionals       pels

          ListIteration


             boolean     hasPrevious();

             Object    previous();

            int   nextIndex(       );

            int   previousIndex(         );





      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            67
```

<details>
<summary>Ver página original</summary>

![Página 67 de Java: colecciones y mapas](img/java-colecciones/pagina-067.webp)

</details>

## Página 68

```text
-  Exemple      de  mètode     que   imprimeix      tots  els elements      d’una   col·lecció:


     static     void   printAll      (Collection       coll)    {

       Iterator     iter    =  coll.iterator(         );

       while    (iter.hasNext(        ))   {
           System.out.println(iter.next(                 )  );

       }

     }


  -  Observeu      que   el codi  és  polimòrfic,     és a  dir, que  funcionarà      per

     qualsevol     col·lecció.


  -  Hi  ha  constructores      de   iteradors   específics    per   llistes:

        ListIterator    listIterator(    );

       ListIterator    listIterator(int     index);

     la darrera    comença      en  la posició   index


      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           68
```

<details>
<summary>Ver página original</summary>

![Página 68 de Java: colecciones y mapas](img/java-colecciones/pagina-068.webp)

</details>

## Página 69

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           69
```

<details>
<summary>Ver página original</summary>

![Página 69 de Java: colecciones y mapas](img/java-colecciones/pagina-069.webp)

</details>

## Página 70

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            70
```

<details>
<summary>Ver página original</summary>

![Página 70 de Java: colecciones y mapas](img/java-colecciones/pagina-070.webp)

</details>

## Página 71

```text
Cues
       -

          Piles
       -

          ...
       -




















      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            71
```

<details>
<summary>Ver página original</summary>

![Página 71 de Java: colecciones y mapas](img/java-colecciones/pagina-071.webp)

</details>

## Página 72

```text
public          interface              Queue<E>             extends

         Collection<E>                   {


              E    element();                                   //throws


              E    peek();                                      //null

              boolean            offer(E           e);          //add        -    bool


              E    remove();                                    //throws

              E    poll();                                      //null


     }









      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            72
```

<details>
<summary>Ver página original</summary>

![Página 72 de Java: colecciones y mapas](img/java-colecciones/pagina-072.webp)

</details>

## Página 73

```text
-  La    classe       java.util.Collections                              té


          molts       mètodes          útils   per    treballar       amb


          col·leccions





          Alguns        dels    algorismes           requereixen
       -

          implementar              pels    teus     objectes        una     interfície

          addicional,          anomenat            Comparable               o


          Comparator.







      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            73
```

<details>
<summary>Ver página original</summary>

![Página 73 de Java: colecciones y mapas](img/java-colecciones/pagina-073.webp)

</details>

## Página 74

```text
-  Són    mètodes        estàtics     que    implementen           algorismes

        usuals     en   llistes:


        -  sort: Ordena     fent servir  mergesort

        -  shuffle:  Barreja   aleatòriament     els elements     de la llista

        -  reverse:   Inverteix  l’ordre

        -  rotate:  Rota   la llista el nombre   de  vegades    que  vulguem


        -  fill: Reescriu  tots  els elements    de  la llista amb  l’element    que  volem.

        -  copy:   Copia  una   llista sobre  una  altra

        -  binarySearch:     Cerca   fent  servir cerca  binaria

        -  indexOfSubList:      Retorna    el índex  de  la primera   subllista  trobada


        -  lastIndexOfSubList:       Retorna   el índex  de  la darrera   subllista  trobada

        -  max:   Retorna    el màxim    de la llista

        -  min:  Retorna    el mínim    de la llista

      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            74
```

<details>
<summary>Ver página original</summary>

![Página 74 de Java: colecciones y mapas](img/java-colecciones/pagina-074.webp)

</details>

## Página 75

```text
Per    ordenar,        trobar       un   element,         trobar       el
       -

          màxim,         etc,    es  necessita         comparar           objectes.


          Definirem          doncs       un    mètode         comparador             de
       -

          objectes,         de   manera         que     donats       2  elements


          retorni       un   enter:


           -  Negatiu:      quan     el primer      sigui   menor      que    el  segon


           -  Zero:    quan     siguin    iguals


           -  Positiu






      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            75
```

<details>
<summary>Ver página original</summary>

![Página 75 de Java: colecciones y mapas](img/java-colecciones/pagina-075.webp)

</details>

## Página 76

```text
S’implementa               la  classe     Comparator             amb
       -

          l´únic     mètode         que     conté,       amb      la  funció      de


          comparació             que    volem       fer   servir


          Utilitzem         la  funció      de    comparació            passant
       -

          una     instancia        de    la  classe     definida        al  mètode


          de    ordenació          o  el  que     sigui.












      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            76
```

<details>
<summary>Ver página original</summary>

![Página 76 de Java: colecciones y mapas](img/java-colecciones/pagina-076.webp)

</details>

## Página 77

```text
public    class    CountComparator          implements      Comparator       {

       public    int   compare(Object         o1,   Object     o2)   {

          if  (o1   !=   null   &&
                o2  !=   null   &&

                o1  instanceof       Count    &&

                o2  instanceof       Count)     {

             Count    c1  =  (Count)     o1;

             Count    c2  =  (Count)     o2;

             return    (c2.i    -  c1.i);

          }  else   {
             return    0;

          }

       }

    }




      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           86
```

<details>
<summary>Ver página original</summary>

![Página 77 de Java: colecciones y mapas](img/java-colecciones/pagina-077.webp)

</details>

## Página 78

```text
public   class  WordFrequency4    {

          static  public  void   main(String[]   args)   {
            ....

            List  list  = new  ArrayList(words.values());
            Collections.sort(list,      new  CountComparator());

            Iterator   iter  = list.iterator();
            while  (iter.hasNext())     {

              count   = (Count)   iter.next();
              word  =  count.word;

              System.out.println(word      +
                   (word.length()    <  8 ?  "\t\t"  : "\t")   +

                   count.i);
            }

          }
       }







      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana            87
```

<details>
<summary>Ver página original</summary>

![Página 78 de Java: colecciones y mapas](img/java-colecciones/pagina-078.webp)

</details>

## Página 79

```text
class  Producte  implements   Comparable   {
         private   String  nom;
         private   int preu;


         public String getNom() {
           return nom;
         }

         public void setnom(String nom) {
           this.nom = nom;
         }

         public int getPreu() {
           return preu;
         }

         public void setPreu(String preu) {
           this.preu = preu;
         }

         public int compareTo(Object anotherProducte) throws ClassCastException {
           if (!(anotherPerson instanceof Producte))
             throw new ClassCastException("A Producte object expected.");
           int anotherProductePreu = ((Producte) anotherProducte).getPreu();
           return this.preu - getPreu;
         }
       }


      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           88
```

<details>
<summary>Ver página original</summary>

![Página 79 de Java: colecciones y mapas](img/java-colecciones/pagina-079.webp)

</details>

## Página 80

```text
Crear      classe      futbolista
       -

           -  Nom


           -  Gols


           -  Assistències



           -  Comparable

              ▪ Nombre      de  gols


              ▪ En   cas  d’empat     nombre     d’assistències


              ▪ En   cas  d’empat     nom

          Crear      una     col·lecció        de   futbolistes         i ordenar
       -



      PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           89
```

<details>
<summary>Ver página original</summary>

![Página 80 de Java: colecciones y mapas](img/java-colecciones/pagina-080.webp)

</details>

## Página 81

```text
PROP 2022-2023 Q2      Mario Martin – Ignasi Gómez Sebastià - Bernat Orellana           90
```

<details>
<summary>Ver página original</summary>

![Página 81 de Java: colecciones y mapas](img/java-colecciones/pagina-081.webp)

</details>

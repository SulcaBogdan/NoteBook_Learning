# Crearea unui linked list

Primul pas este sa definim clasa pentru nod care va contine cele doua proprietati, respectiv data(informatia) si referinta catre urmatorul nod:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
```

Am definit clasa `Node` cu constructorul care primeste ca argument `data` si o proprietate initializata `next` care reprezinta un pointer sau o referinta catre urmatorul nod din lista.

Dupa crearea clasei pentru noduri urmeaza sa definim clasa pentru LinkedList.

```python
class LinkedList:
    def __init__(self):
        self.head = None
```

Am definit clasa `LinkedList` pentru a initializa o lista goala. `self.head = None` indica faptul ca la inceput, lista nu contine nici un element. Acum ca avem clasa pentru nod si clasa pentru LinkedList trebuie doar sa adaugam metode pentru adaugare , stergere, inlocuire etc.

## Inserare intr-un linked list

Exemplu de metoda pentru inserarea unui nod la inceputul linked list:

```python
def insertAtBegin(self, data):
    new_node = Node(data)
    if self.head is None:
        self.head = new_node
        return
    else:
        new_node.next = self.head
        self.head = new_node
```

Aceasta metoda primeste ca argument `data` care reprezinta valoarea pe care vrem sa o adaugam in lista.

Initializam un obiect de `Node` cu denumirea `new_node` si ca paramentru introducem valoarea `data` din metoda.

Verificam daca `head` exista (daca este None), daca `head` este `None` atunci obiectul node (valoarea noastra) va devenii `head`, si oprim metoda, dar daca `head` exista deja (nu este `None`) atunci vom lega referinta lui `new_node` spre `self.head` apoi vom spune ca `new_node` = `self.head` adica mai simplu am legat noua valoare la prima valoare initiala si am mutat `head` pe valoarea noua. 

Exemplu. Vrem sa adaugam 7 la primul element. `->` reprezinta referintele dintre noduri.

`1(head) -> 2 -> 3`   `7->`

Leaga referinta lui 7 cu primul element `7 -> 1(head) -> 2 -> 3` (`new_node.next = self.head`)

Mutam head-ul la primul element actual `7(head) -> 1 -> 2 -> 3` (`self.head = new_node`)

Cand spunem `.next` este vorba despre `->` adica despre referinta nodului(catre ce arata).


Acesta a fost un exemplu de adaugare a unui `nod`(valoarea noastra) la inceputul listei.

### Putem insera un nod intr-o pozitie specifica intr-un linked list? Da!

## Inserarea intr-o pozitie specifica din linked list.

```python
def insertAtIndex(self, data, index):
    new_node = Node(data)
    current_node = self.head
    position = 0
    if position == index:
        self.insertAtBegin(data)
    else:
        while(current_node != None and position+1 != index):
            position += 1
            current_node = current_node.next

        if current_node != None:

            new_node.next = current_node.next
            current_node.next = new_node
        else:
            print("Index not present")
```

Aceasta metoda se foloseste si de metoda create mai sus respectiv `insertAtBegin`.

Am definit metoda `insertAtIndex` care primeste 2 argumente `data` si `index`. `data` reprezinta valoarea pe care noi vrem sa o introducem iar `index` reprezinta locatia unde vrem sa inseram elementul.

La fel ca la metoda de mai sus incepem prin a crea un nou obiect de `Node`. Apoi stabilim nodul curent `current_node` cu primul element din lista (`head`).
Initializam variabila `position` cu  0 care reprezinta pozitia elementelor din lista.

Daca `index` = `position`(0) adica 0 = 0 ne folosim de metoda `insertAtBegin` pentru a adauga primul element in linked list.

Daca `index` =! `position`(0) atunci cream un while loop care are ca conditii urmatoarele:

Nodul curent `current_node` sa nu fie `None` adica lista sa nu fie goala si `position + 1` sa nu fie `=` cu `index` pe care l-am ales noi, adica daca `position + 1` `=` `index` atunci loop-ul se opreste. Daca conditiile nu sunt indeplinite vom incrementa 1 la variabila `position` pana cand aceasta va fi `=` cu `index`, si vom parcurge prin lista spunand `current_node` `=` `current_node.next` adica urmatorul element din lista.

In conlcuzie while loop-ul se va opri cand una dintre cele doua conditii vor fi indeplinite. Daca prima conditie va fi indeplinita rezulta ca am ajuns la sfarsitul listei si nu s-a gasit indexul, iar daca a doua conditie se indeplineste rezulta ca s-a gasit index-ul si loop-ul se opreste.

Dupa ce loop-ul se opreste mai facem o verificare sa vedem rezultatul. Verificam, daca nodul curent `current_node` nu este `None`. 

Daca acesta nu este `None` inseamna ca `position+1` = `index` din loop , adica am gasit indexul pe care il cautam si elementul de pe acesta. Asadar atribuim `new_node.next` sa fie egal cu `current_node.next` adica referinta noului nod va fi egala cu referinta initiala a `current_node`. Mai simplu `new_node` pe care vrem noi sa il adaugam pe indexul gasit va arata catre acelasi nod care `current_node` arata precedent. Apoi `current_node` va arata spre `new_node` astfel finalizant inserarea. 

`1 -> 2 -> 3 -> 4` vrem sa adaugam 7 pe indexul 2 asadar `current_node` `=` `2` care are pointer spre `3` si ca noi sa adaugam elementul 7 pe indexul 2 vom spune ca `new_node.next` `=` `current_node.next` adica pointerul lui `new_node` `=` pointerul lui `current_node` `=` `3`, apoi spunem ca `current_node.next` `=` `new_node` adica pointerul lui `current_node` va arata spre `new_node`.  Rezultatul final este `1 -> 2 -> 7 -> 3 -> 4`.


### Am inserat la inceput , la un index ales putem insera si la final!

## Inserarea la finalul unui linked list

```python
def insertAtEnd(self, data):
    new_node = Node(data)
    if self.head is None:
        self.head = new_node
        return
    else:
        current_node = self.head
        while(current_node != None):
            current_node = current_node.next

        current_node.next = new_node
```

Avem o metoda de inserare a unui nod la finalul unui Linked list. Metoda se numeste `insertAtEnd` si accepta ca argument `data` care reprezinta valoarea noastra pe care vrem sa o adaugam.

Primul pas ca in orice metoda de adaugare/inserare a unei valori este sa creeam un obiect de `Node` `new_node` care accepta `data` ca argument si reprezinta valoarea noastra.

Verificam daca lista noastra are elemente pentru a fi eficienti in rulare. Deci spunem ca `if self.head is None` adica daca lista nu are elemente atunci `self.head = new_node` si `return` pentru a opri metoda.

Dar daca `self.head` nu este `None` atunci inseamna ca avem elemente in lista si pentru a gasi ultimul element va trebuii sa iteram prin lista. Pentru inceput trebuie sa alegem un punct de pornire iar cel mai potrivit este primul element din lista respectiv `self.head`. Spunem ca `current_node` `=` `self.head` adica selectam primul element din lista.

Pentru a itera prin lista folosim un `while` loop cu conditia de oprire ca `current_node` sa fie `None` adica ultimul element sa aibe referinta spre `None`. Cand aceasta conditie este `True` atunci loop-ul se opreste si adaugam ultimul element.

`current_node.next` `=` `new_node` adica referinta ultimului element din lista arata spre `new_node` adica elementul nostru.

Exemplu 

`1(head) -> 2 -> 3 -> 4` vrem sa adaugam la final 5

iteram prin lista si ajungem la `4` unde spunem ca `4(current_node) ->(current_node.next) 5(new_node)` 

Rezultatul final este `1 -> 2 -> 3 -> 4 -> 5`

Deci am invatat sa adaugam la inceput un element , la un index ales si la final. Dar daca vreau sa modific un element deja existent?

## Modificarea unui Node din Linked list

```python
def updateNode(self, val, index):
    current_node = self.head
    position = 0
    if position == index:
        current_node.data = val
    else:
        while(current_node != None and position != index):
            position +=1
            current_node = current_node.next

        if current_node != None:
            current_node.data = val
        else:
            print('index not found')
```

Am definit metoda `updateNode` care accepta doua argumente, `val` pentru valoarea pe care vrem sa o suprascriem si `index` care reprezinta indexul elementului din lista pe care vrem sa il inlocuim.


Pentru a cauta index-ul din lista va trebuii sa parcurgem lista, de aceea initializam variabila `current_node` cu `self.head` adica incepem iteratia de la primul element din lista. Initializam si variabila `position` cu `0` care reprezinta de la ce valoare incepe numaratoare adica de la indexul 0.

Verificam daca lista are elemente pentru a nu folosi resurse degeaba folosind un `if statement`. Spunem daca `position` `=` `index` adica daca indexul pe care l-am pus ca argument este `0` atunci prima valoare din lista va avea valoarea pusa de noi.

Exemplu

`1 -> 2 -> 3` indexul ales `=` `0` si valoarea de inlocuit `=` `4`

Verificam daca `position` `=` `index` adica daca `0` `=` `0` True.

Atunci `current_node.data` `=` `val` adica valoarea elementului initial va devenii valoarea pusa de noi.

Rezultat
`4 -> 2 -> 3`

Daca indexul ales de noi este mai mare ca 0 atunci vom parcurge lista cu un `while loop` pana cand vom gasii indexul dorit.

Conditiile sunt ca `current_node` `!=` `None` adica daca `current_node` `->` `None` se va oprii loop-ul si indexul nu a fost gasit si conditia ca `position` `!=` `index` adica daca `position` `=` `index` se va oprii loop-ul si inseamna ca indexul a fost gasit iar valoarea va fi inlocuita mai departe.

## Stergerea unui Node in Linked list

### Stergerea primului element din lista

Putem sterge primul element dintr-un Linked List prin a atribui celui de al doilea element din Linked list pozitia de `head`.

Exemplu:

```python
def remove_first_node(self):
    if(self.head == None):
        return
    else:
        self.head = self.head.next      
```

Am creat o metoda `remove_first_node` care nu primeste nici un argument. Verificam daca `head` este None si daca conditia este indeplinita vom opri metoda deoarece lista este goala, dar daca nu este `None` atunci vom spune ca `head` `=` `head.next` adica noul `head` va fi elementul catre care precedentul `head` avea referinta.

`1(head) -> 2 -> 3` vrem sa stergem primul element adica `1`

Spunem ca `1(head)` `=` `-> 2` adica `1` va fi sters si va ramane doar `2` noul `head`

Rezultat

`2(head) -> 3`

### Stergerea ultimului element din lista

```python
def remove_last_node(self):
    if self.head is None:
        return
    current_node = self.head
    while(current_node.next.next):
        current_node = current_node.next
    current_node.next = None
```

Am definit o metoda `remove_last_node` care nu primeste nici un argument.

Am verificat daca lista este goala cu un `if statement` . Daca `head` este `None` atunci lista este goala si oprim rularea metodei.

Daca lista nu este goala atunci va trebuii sa iteram prin ea incepand de la primul element pentru a gasi ultimul element. Asadar initializam variabila `current_node` cu `self.head` adica `current_node` este primul element din lista.

Vom parcurge lista cu un `while loop` care are ca conditie ca `current_node.next.next` sa fie `True` adica vom verifica referinta din 2 in 2 si atunci cand o referinta este `None` se va opri loop-ul. Pana cand aceasta conditie nu o sa mai fie `True` vom spune ca `current_node` `=` `current_node.next` adica vom parcurge elementele.

La final vom spune ca penultimul element din lista se va referii la `None` astfel ultimul element din lista va devenii `None`.

`1 -> 2 -> 3` vrem sa-l stergem pe 3. Vom itera prin lista cand referinta dubla va arata catre `None`.

`current_node.next.next` adica daca incepem de la `1` noi verificam daca exita referinta la o valoare de 2 ori adica  `1` `->` `2` `True`, `2` `->` `3` `True`, rezultatul conditiei este `True` asadar se executa blocul `while` si vom trece la urmatorul element din lista adica `2`. Dinou se verifica conditia `2` `->` `3` `True`, `3` `->` `None` `False`, deoarece ultima verificare este `False` atunci loop-ul se opreste si la final vom ramane cu `current_node` `=` `2`.

Dupa ce s-a oprit loop-ul pentru a sterge ultimul element vom spune ca `current_node` `=` `None` adica `2` `->` `None` (care era 3 inainte.)

Se foloseste `current_node.next.next` doarece vrem sa ajungem la penultimul element din lista care are referinta catre ultimul element pe care vrem sa il stergem.

### Stergerea unui element la un index ales din Linked list

```python
def remove_at_index(self, index):
    if self.head == None:
        return
    current_node = self.head
    position = 0
    if position == index:
        self.head = self.head.next
    else:
        while(current_node != None and position+1 != index):
            position += 1
            current_node = current_node.next
    
    if current_node != None:
        current_node.next = current_node.next.next
    else:
        print('index not found')
```

Am definit o metoda numita `remove_at_index` care accepta ca argument `index` care reprezinta index-ul elementului pe care vrem sa il stergem din lista. 

Pentru inceput verificam daca lista are elemente printr-un `if statement`. Daca lista este goala oprim metoda din functionare.

Daca lista nu este goala atunci initializam variabila `current_node` `=` `self.head` adica selectam primul nod din lista (head) si initializam si variabila `position` `=` `0` care reprezinta index-ul elementelor din lista.

Mai adaugam o verificare in cazul in care alegem indexul 0 cu un `if statement`. Daca `position` `=` `index` adica `0` `=` `0` atunci stergem primul element din lista ca in metoda de mai sus.

Dar daca `index` `!=` `0` atunci parcurgem lista incepand de la primul element folosind `while loop`. Conditiile sunt ca `current_node` `!=` `None` adica nodul curent sa existe si `position+1` `!=` `index` adica pozitia din lista + 1 sa fie diferita de `index`. Daca una dintre cele doua conditii devine `Flase` atunci loop-ul va inceta. Daca prima conditie este `False` rezulta ca nu s-a gasit indexul in lista iar daca a doua conditie este `False` rezulta ca s-a gasit indexul.

Se mai face o verificare cu un `if statement` pentru a vedea rezultatul loop-ului. Daca indexul a fost gasit atunci spunem ca `current_node.next` `=` `current_node.next.next` adica sarim peste elementul dintre cele doua elemente.


`1 -> 2 -> 3 -> 4` vrem sa stergem elementul `2` de pe indexul `1`

Se verifica lista daca este goala ceea ce nu este deci mergem mai departe, apoi se verifica daca indexul nostru `1` `=` `position` adica cu `0` ceea ce este `False` deci mergem mai departe si intram in `while loop`.

Se verifica prima conditie `current_node` `!=` `None` adica `1` `!=` `None` `True`. Se verifica si a doua conditie `position+1` `!=` `index` adica `1` `!=` `1` care este `False` deci loop-ul se va opri aici.

Verificam la final daca elementul de pe `current_node` nu este `None` ceea ce este `True` si intram in blocul `if statement` unde spunem ca `current_node.next` `=` `current_node.next.next` adica `1(current_node) ->(current_node.next) ->(current_node.next.next) -> 3 -> 4`. Tot ce facem este sa setam referinta lui `1` peste nodul cu valoarea `2` direct spre nodul cu valoare `3`. Iar in proces nodul cu valoarea `2` va fi sters.

Rezultat

`1(head) -> 3 -> 4`

Am sters un nod dupa index, dar putem sterge un nod dupa valoare? Da!

### Stergerea unui nod dupa valoarea sa 

```python
def remove_at_value(self, data):
    if self.head is None:
        return
    
    current_node = self.head

    if current_node.data == data:
        current_node = current_node.next
        return
    
    while(current_node != None and current_node.next.data != data):
        current_node = current_node.next

    if current_node == None:
        return
    else:
        current_node.next = current_node.next.next
```

Am definit metoda `remove_at_value` care accepta ca argument `data` care reprezinta valoare pe care vrem sa o gasim in lista.

Pentru inceput verificam daca lista este goala cu un `if statement`. Daca aceasta este goala folosim `return` pentru a opri functionarea metodei, dar daca nu este goala atunci mergem mai departe.

Initializam variabila `current_node` cu `self.head` care reprezinta primul element din lista noastra.

Verificam daca valoarea primului element din lista este `=` cu valoarea introdusa de noi printr-un `if statement` . `if current_node.data == data:` adica 'Daca valoarea nodului curent este `=` cu valoarea introdusa de noi `data`' atunci sterge primul element din lista prin `current_node` `=` `current_node.next` adica `current_node` care este `self.head` va fi egala cu referinta acestuia adica urmatorul element din lista mai exact `current_node.next`


Daca valoarea lui `current_node.data` nu este egala cu `data` atunci mergem mai departe.

Pentru a itera folosim `while loop` cu conditiile ca `current_node` sa nu fie `None` si `current_node.next.data` sa nu fie egala cu `data` . Daca prima conditie este `False` rezulta ca s-a ajuns la sfarsitul listei si valoarea `data` nu a fost gasita iar daca a doua conditie este `False` rezulta ca s-a gasit nodul cu valoarea lui `data`. In oricare conditie daca este `False` loop-ul se va opri.

Dupa verificam rezultatul `while loop` printr-un `if statement` . Daca `current_node` `=` `None` adica daca nu s-a gasit `data` in lista `return` ca sa oprim metoda. Altfel `current_node.next` `=` `current_node.next.next` adica mutam referinta de pe `current_node.next` pe urmatorul element `current_node.next.next` astfel stergand elementul cu valoarea noastra in proces.

`1 -> 2 -> 3 -> 4 -> 5` vrem sa stergem elementul cu valoarea `4`

Verificam daca lista este goala, ceea ce nu este deci mergem mai departe.

Verificam daca `4` este primul element din lista, adica `1` `=` `4` ? `False`, mergem mai departe.

Iteram prin lista pana ajungem la nodul cu valoarea 4. Procesul ar arata cam asa. Facem un `while loop` cu cele 2 conditii de mai sus si verificam fiecare conditie in parte. Prima conditie `current_node != None`? adica `1 != None`? `True`, urmatoarea conditie `current_node.next.data != data`? adica `current_node_next` este referinta primului element catre al doilea element adica `1` `->` `2`, deci cand spunem `.data` ne referim la valoarea al doilea element din lista care este `2`. Deci `2` != `4`? `True` intram in blocul `while` si parcurgem la urmatorul element prin `current_node` = `current_node.next`.

Intram iar in `while loop` si verificam iar conditiile. `current_node != None` adica `2 != None` `True` , verificam si a doua conditie `current_node.next.data != data ` adica `3 != 4` `True`. Intram iar in blocul `while` si parcurgem mai departe elementul din lista cu `current_node` `=` `current_node.next` adica `2` `=` `3`.

Revenim iar la `while loop` unde se verifica iar conditiile. Prima conditie `current_node != None` adica `3 != None` `True`, verificam si a doua conditie `current_node.next.data != data` adica `4 != 4` `False`. Aici se va opri iteratia si vom merge mai departe deoarece nu s-a mai respectat ultima conditie insemnand ca s-a gasit elementul cu valoarea `4`.

Verificam la final rezultatul cu un `if statement` unde spunem ca `current_node.next` adica `3` `=` `current_node.next.next` adica `5` . Deci in acest proces elementul cu valoarea `4` va fi sters.

Rezultat

`1(head) -> 2 -> 3 -> 5`
``
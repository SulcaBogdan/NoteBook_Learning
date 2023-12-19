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
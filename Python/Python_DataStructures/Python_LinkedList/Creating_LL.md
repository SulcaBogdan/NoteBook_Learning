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

Verificam daca `head` exista (daca este None), daca `head` este `None` atunci obiectul node (valoarea noastra) va devenii `head`, si oprim metoda, dar daca `head` exista deja (nu este `None`) atunci vom atribui urmatoarului nod din lista valoarea lui `head` si noul `head` va devenii `new_node` valoarea introdusa de noi.

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
        while(current_node != None and position != index):
            position += 1
            current_node = current_node.next
            `1 -> 2 -> 3 -> 4`

        if current_node != None:

            new_node.next = current_node.next
            current_node.next = new_node
        else:
            print("Index not present")
```

Aceasta metoda se foloseste si de metoda create mai sus respectiv `insertAtBegin`.

Am definit metoda `insertAtIndex` care primeste 2 argumente `data` si `index`. `data` reprezinta valoarea pe care noi vrem sa o introducem iar `index` reprezinta locatia unde vrem sa inseram elementul.

La fel ca la metoda de mai sus incepem prin a crea un nou obiect de `Node`. Apoi stabilim nodul curent `current_node` cu primul element din lista (`head`).
Initializam variabila `position` cu  0 care reprezinta indexul 0 al listei.

Daca `index` = `position`(0) adica 0 = 0 ne folosim de metoda `insertAtBegin` pentru a adauga primul element in linked list.

Daca `index` =! `position`(0) atunci cream un while loop care are ca conditii urmatoarele:

Nodul curent `current_node` sa nu fie `None` adica lista sa nu fie goala si `position + 1` sa nu fie = cu `index` pe care l-am ales noi, adica daca `position` = `index` atunci loop-ul se opreste. Daca conditiile nu sunt indeplinite vom itera 1 la variabila `position` pana cand aceasta va fi `=` cu `index`, si nodul curent `current_node` va fi egal cu `current_node.next` adica vom selecta urmatorul node din lista.

In conlcuzie while loop-ul se va opri cand una dintre cele doua conditii vor fi indeplinite. Daca prima conditie va fi indeplinita rezulta ca am ajuns la sfarsitul listei si nu s-a gasit indexul, iar daca a doua conditie se indeplineste rezulta ca s-a gasit index-ul si loop-ul se opreste.

Dupa ce loop-ul se opreste mai facem o verificare sa vedem rezultatul. Verificam, daca nodul curent `current_node` nu este `None`. 

Daca acesta nu este `None` inseamna ca `position` = `index` din loop , adica am gasit indexul pe care il cautam si elementul de pe acesta. Asadar atribuim `new_node.next` sa fie egal cu `current_node.next` adica referinta noului nod va fi egala cu referinta initiala a `current_node`. Mai simplu `new_node` pe care vrem noi sa il adaugam pe indexul gasit va arata catre acelasi nod care `current_node` arata precedent. Apoi `current_node` va arata spre `new_node` astfel finalizant inserarea. 

`1 -> 2 -> 3 -> 4` vrem sa adaugam 7 pe indexul 2 asadar `current_node` = `3` care are pointer spre `4` si ca noi sa adaugam elementul 7 pe indexul 2 vom spune ca `new_node.next` = `current_node.next` adica pointerul lui `new_node` = pointerul lui `current_node` = `4`, apoi spunem ca `current_node.next` = `new_node` adica pointerul lui `current_node` va arata spre `new_node`. si rezultatul final este `1 -> 2 -> 3 -> 7 -> 4`.



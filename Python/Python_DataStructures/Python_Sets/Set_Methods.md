# Metodele Set-ului

| Metodă                  | Descriere                                                                           | Exemplu                                                                                                   |
|-------------------------|-------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| add()                   | Adaugă un element în set                                                           | `set_exemplu = {1, 2, 3}` <br> `set_exemplu.add(4)` <br> `print(set_exemplu)` va afișa `{1, 2, 3, 4}`        |
| clear()                 | Elimină toate elementele din set                                                    | `set_exemplu = {1, 2, 3}` <br> `set_exemplu.clear()` <br> `print(set_exemplu)` va afișa `set()`              |
| copy()                  | Returnează o copie a set-ului                                                      | `set_exemplu = {1, 2, 3}` <br> `copie_set = set_exemplu.copy()`                                           |
| difference()            | Returnează un set care conține diferența dintre două sau mai multe set-uri          | `set1 = {1, 2, 3}` <br> `set2 = {3, 4, 5}` <br> `rezultat = set1.difference(set2)` <br> `print(rezultat)` va afișa `{1, 2}`  |
| difference_update()     | Elimină elementele din acest set care sunt, de asemenea, incluse în alt set specificat | `set1 = {1, 2, 3}` <br> `set2 = {3, 4, 5}` <br> `set1.difference_update(set2)` <br> `print(set1)` va afișa `{1, 2}`  |
| discard()               | Elimină elementul specificat                                                        | `set_exemplu = {1, 2, 3}` <br> `set_exemplu.discard(2)` <br> `print(set_exemplu)` va afișa `{1, 3}`           |
| intersection()          | Returnează un set, adică intersecția dintre două set-uri                            | `set1 = {1, 2, 3}` <br> `set2 = {2, 3, 4}` <br> `rezultat = set1.intersection(set2)` <br> `print(rezultat)` va afișa `{2, 3}` |
| intersection_update()   | Elimină elementele din acest set care nu sunt prezente în alte set-uri specificate | `set1 = {1, 2, 3}` <br> `set2 = {2, 3, 4}` <br> `set1.intersection_update(set2)` <br> `print(set1)` va afișa `{2, 3}` |
| isdisjoint()            | Returnează dacă două set-uri au sau nu o intersecție                               | `set1 = {1, 2, 3}` <br> `set2 = {4, 5, 6}` <br> `rezultat = set1.isdisjoint(set2)` <br> `print(rezultat)` va afișa `True` |
| issubset()              | Returnează dacă un alt set conține sau nu acest set                                | `set1 = {1, 2}` <br> `set2 = {1, 2, 3, 4}` <br> `rezultat = set1.issubset(set2)` <br> `print(rezultat)` va afișa `True`   |
| issuperset()            | Returnează dacă acest set conține sau nu un alt set                               | `set1 = {1, 2, 3, 4}` <br> `set2 = {1, 2}` <br> `rezultat = set1.issuperset(set2)` <br> `print(rezultat)` va afișa `True`   |
| pop()                   | Elimină un element din set                                                          | `set_exemplu = {1, 2, 3}` <br> `element = set_exemplu.pop()` <br> `print(element)` va afișa un element și `set_exemplu` va conține restul |
| remove()                | Elimină elementul specificat                                                        | `set_exemplu = {1, 2, 3}` <br> `set_exemplu.remove(2)` <br> `print(set_exemplu)` va afișa `{1, 3}`             |
| symmetric_difference()  | Returnează un set cu diferențele simetrice dintre două set-uri                     | `set1 = {1, 2, 3}` <br> `set2 = {3, 4, 5}` <br> `rezultat = set1.symmetric_difference(set2)` <br> `print(rezultat)` va afișa `{1, 2, 4, 5}` |
| symmetric_difference_update() | Inserează diferențele simetrice din acest set și un alt set | `set1 = {1, 2, 3}` <br> `set2 = {3, 4, 5}` <br> `set1.symmetric_difference_update(set2)` <br> `print(set1)` va afișa `{1, 2, 4, 5}` |
| union()                 | Returnează un set conținând uniunea dintre set-uri                                 | `set1 = {1, 2, 3}` <br> `set2 = {3, 4, 5}` <br> `rezultat = set1.union(set2)` <br> `print(rezultat)` va afișa `{1, 2, 3, 4, 5}` |
| update()                | Actualizează set-ul cu uniunea dintre acest set și altele                         | `set1 = {1, 2, 3}` <br> `set2 = {3, 4, 5}` <br> `set1.update(set2)` <br> `print(set1)` va afișa `{1, 2, 3, 4, 5}` |
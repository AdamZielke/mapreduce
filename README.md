ZADANIE 3
=====

### Anagramy
### Tytuł: Użycie Map Reduce w MongoDB

=====


|Specyfikacja komputera |                                         |
|-----------------------|-----------------------------------------|
| System operacyjny     | Windows 7 (64-bit)             |
| Procesor              | Intel(R) Core(TM) i5-1337M CPU @ 2.40GHz|
| Pamięć Ram            | 4 GB                                    |
| Dysk twardy           | 500 GB                               |


[word_list.txt](http://wbzyl.inf.ug.edu.pl/nosql/doc/data/word_list.txt) 
Zostało zaimporotowane do bazy MongoDB

W celu importu skorzystałem z polecenia:
```sh
mongoimport -d anagrams -c anagrams --type csv --file D:/dane/word_list.txt -f "words"
```

Czas wykonania operacji: 0,758 sekundy.

Zaimportowano:
```sh
> db.anagrams.count()
8199
```
Anagramy uzyskałem z użyciem mapreduce:
Pary posortowanych słów oraz ciągów znaków. 
```sh
db.anagrams.mapReduce(
  function(){emit(Array.sum(this.words.split("").sort()), this.words);},
  function(key, values) {return values.toString()},
  {
    query: {},
    out: "result"
  }
)



```
![obraz](http://thewindowsclub.thewindowsclubco.netdna-cdn.com/wp-content/uploads/2011/11/SQL-600x309.png?75a050)

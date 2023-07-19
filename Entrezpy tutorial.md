# ENTREZPY TUTORIAL

## Czym jest Entrezpy?

Entrezpy to dedykowana biblioteka w Pythonie do interakcji z bazami danych NCBI poprzez E-Utilities.

## Instalacja

```bash
pip install entrezpy
```

## INQUIRE()

Służy do wysłania zapytania do bazy danych Entrez i pobrania wyników wyszukiwania na podstawie określonych parametrów. Pozwala użytkownikom wyszukiwać rekordy spełniające określone kryteria w bazie danych i uzyskiwać odpowiednie informacje do dalszego przetwarzania lub analizy.
Wykorzystuje dane pobrane za pomocą funkcji zawartej w paczce wykorzystującej E-Utility.

```Python

data.inquire({'db' : 'pubmed',
              'id' : [17284678, 9997],
              'retmode' : 'text',
              'rettype' : 'abstract'})

```

### Parametry funkcji wykorzystujących E-Utility:

**tool** - Nazwa narzędzia, do którego należy żądanie

**email** - Kompletny i prawidłowy adres e-mail należący do twórcy oprogramowania, a nie użytkownika końcowego będącego osobą trzecią.

**apikey** - NCBI API Key

**apikey_var** - Zmienna środowiskowa przechowująca NCBI API Key

**threads** - liczba wątków

**qid** - Unikalny identyfikator zapytania Esearch. Zostanie wygenerowany, jeśli nie zostanie podany.

## ESEARCHER

**entrezpy.esearch.esearcher.Esearcher** implementuje narzędzie E-utility ESearch. Esearcher wykonuje zapytania, zwracając identyfikatory UID dla danych w żądanej bazie danych Entrez lub odwołania WebEnv/QueryKey z serwera Historii Entrez.

### Wspierane parametry E-Utility


| **_Narzędzie_** 	| **_Parametr_** 	|             **_Typ_**             	|                                                   **_Opis_**                                                   	|
|:---------------:	|:--------------:	|:---------------------------------:	|:--------------------------------------------------------------------------------------------------------------:	|
| **Esearcher**   	|                	|                                   	|                                                                                                                	|
|                 	|     **db**     	|               _str_               	| Baza danych do wyszukania (np.: "PubMed", "Protein", "Gene", "Nucleotide")                                     	|
|                 	|   **WebEnv**   	|               _str_               	| Pozwala na połączenie sesji wyszukiwania, umożliwiając żądaniom na dostęp do historii wyszukiwania czy wyników 	|
|                 	|  **query_key** 	|               _int_               	| Identyfikuje określone zapytanie w ramach sesji wyszukiwania                                                   	|
|                 	|   **uilist**   	|               _bool_              	| Zwraca listę unikalnych identyfikatorów (UIDs)                                                                 	|
|                 	|   **retmax**   	|               _int_               	| Maksymalna liczba pobranych rekordów (np. 110000)                                                              	|
|                 	|  **retstart**  	|               _int_               	| Określa indeks pierwszego rekordu do pobrania z wyników wyszukiwania                                           	|
|                 	| **usehistory** 	|               _bool_              	| Użycie serwera historii Entrez.                                                                                	|
|                 	|    **term**    	|               _str_               	| Zapytanie do bazy (np. "viruses[orgn]")                                                                        	|
|                 	|    **sort**    	|               _str_               	| Kolejność sortowania                                                                                           	|
|                 	|    **field**   	|               _str_               	| Zawęża wyszukiwanie do określone pola w bazie danych takich jak: tytuł, autor                                  	|
|                 	|   **reldate**  	|               _int_               	| Umożliwia wyszukiwanie rekordów we względnym zakresie dat np. ostatnie X dni od dnia dzisiejszego              	|
|                 	|  **datetype**  	| _str (YYYY/MM/DD, YYYY/MM, YYYY)_ 	| Typ daty do wyszukania (np. "pdat" dla daty publikacji)                                                        	|
|                 	|   **mindate**  	| _str (YYYY/MM/DD, YYYY/MM, YYYY)_ 	| Minimalna data wyszukania                                                                                      	|
|                 	|   **maxdate**  	| _str (YYYY/MM/DD, YYYY/MM, YYYY)_ 	| Maksymalna data wyszukania                                                                                     	|
|                 	|   **idtype**   	|               _bool_              	| Typ identifikatora używany do pobierania danych np. PMID, Genbank Accession                                    	|
|                 	|   **retmode**  	|   _`json, enforced by Esearcher_  	| Określa format pobranych danych np.: XML, text, JSON                                                           	|
|                 	|   **reqsize**  	|               _int_               	| Określa ilość rekordów żądanych lub przetwarzanych                                                             	|
|                 	|                	|                                   	|                                                                                                                	|


```python

import entrezpy.esearch.esearcher

e = entrezpy.esearch.esearcher.Esearcher(tool = "esearcher", email = "zuzwaw5@st.amu.edu.pl")

a = e.inquire({'db': 'nucleotide',
                'term':'viruses[orgn]',
                'retmax': 110000,
                'rettype': 'uilist'})

print(a.get_result().uids)

```

## EFETCHER

**entrezpy.efetch.efetcher.Efetcher** implementuje narzędzie E-utility EFetch. Efetcher wykonuje zapytania, zwracając dane z serwera Historii Entrez.

### Wspierane parametry E-Utility

| **_Narzędzie_** 	| **_Parametr_** 	|             **_Typ_**             	|                                                   **_Opis_**                                                   	|
|:---------------:	|:--------------:	|:---------------------------------:	|:--------------------------------------------------------------------------------------------------------------:	|
| **Efetcher**    	|                	|                                   	|                                                                                                                	|
|                 	|     **db**     	|               _str_               	| Baza danych do wyszukania (np.: "PubMed", "Protein", "Gene", "Nucleotide")                                     	|
|                 	|   **WebEnv**   	|               _str_               	| Pozwala na połączenie sesji wyszukiwania, umożliwiając żądaniom na dostęp do historii wyszukiwania czy wyników 	|
|                 	|  **query_key** 	|               _int_               	| Identyfikuje określone zapytanie w ramach sesji wyszukiwania                                                   	|
|                 	|   **uilist**   	|               _bool_              	| Zwraca listę unikalnych identyfikatorów (UIDs)                                                                 	|
|                 	|   **retmax**   	|               _int_               	| Maksymalna liczba pobranych rekordów (np. 110000)                                                              	|
|                 	|  **retstart**  	|               _int_               	| Określa indeks pierwszego rekordu do pobrania z wyników wyszukiwania                                           	|
|                 	| **usehistory** 	|               _bool_              	| Użycie serwera historii Entrez.                                                                                	|
|                 	|    **term**    	|               _str_               	| Zapytanie do bazy (np. "viruses[orgn]")                                                                        	|
|                 	|    **sort**    	|               _str_               	| Kolejność sortowania                                                                                           	|
|                 	|    **field**   	|               _str_               	| Zawęża wyszukiwanie do określone pola w bazie danych takich jak: tytuł, autor                                  	|
|                 	|   **reldate**  	|               _int_               	| Umożliwia wyszukiwanie rekordów we względnym zakresie dat np. ostatnie X dni od dnia dzisiejszego              	|
|                 	|  **datetype**  	| _str (YYYY/MM/DD, YYYY/MM, YYYY)_ 	| Typ daty do wyszukania (np. "pdat" dla daty publikacji)                                                        	|
|                 	|   **mindate**  	| _str (YYYY/MM/DD, YYYY/MM, YYYY)_ 	| Minimalna data wyszukania                                                                                      	|
|                 	|   **maxdate**  	| _str (YYYY/MM/DD, YYYY/MM, YYYY)_ 	| Maksymalna data wyszukania                                                                                     	|
|                 	|   **idtype**   	|               _bool_              	| Typ identifikatora używany do pobierania danych np. PMID, Genbank Accession                                    	|
|                 	|   **retmode**  	|   _`json, enforced by Esearcher_  	| Określa format pobranych danych np.: XML, text, JSON                                                           	|
|                 	|   **reqsize**  	|               _int_               	| Określa ilość rekordów żądanych lub przetwarzanych                                                             	|
|                 	|                	|                                   	|                                                                                                                	|



```python

import entrezpy.efetch.efetcher

e = entrezpy.efetch.efetcher.Efetcher(tool="test",
                                      email="zuzwaw5@st.amu.edu.pl",
                                      apikey=None,
                                      apikey_var=None,
                                      threads=None,
                                      qid=None)

analyzer = e.inquire({'db' : 'pubmed',
                      'id' : [17284678, 9997],
                      'retmode' : 'text',
                      'rettype' : 'abstract'})

```


## ELINKER

**entrezpy.elink.elinker.Elinker** implementuje narzędzie E-utility ELink. Elinker wykonuje zapytania, które mogą łączyć wyniki:
- między różnymi bazami danych w ramach Entrez,
- wcześniejsze zapytania na serwerze Historii Entrez,
- do odnośników poza NCBI Entrez, np. do artykułów naukowych.

Elinker zwraca identyfikatory UID dla danych w żądanej bazie danych Entrez lub odwołanie WebEnv/QueryKey z serwera Historii Entrez.

### Wspierane parametry E-Utility


| **_Narzędzie_** 	| **_Parametr_** 	|             **_Typ_**             	|                                                                     **_Opis_**                                                                    	|
|:---------------:	|:--------------:	|:---------------------------------:	|:-------------------------------------------------------------------------------------------------------------------------------------------------:	|
| **Elinker**     	|                	|                                   	|                                                                                                                                                   	|
|                 	|     **db**     	|               _str_               	| Baza danych do wyszukania (np.: "PubMed", "Protein", "Gene", "Nucleotide")                                                                        	|
|                 	|   **dbfrom**   	|               _str_               	| Określa źródłową bazę danych która będzie używana w celu przesyłania do innej bazy danych.                                                        	|
|                 	|     **id**     	|               _list_              	| lista ID używanych do łączenia rekordów w bazach danych Entrez                                                                                    	|
|                 	|     **cmd**    	|               _str_               	| Określa polecenie lub operację do wykonania np.: search, fetch, summary                                                                           	|
|                 	|  **linkname**  	|               _str_               	| Określa rodzaj łącza które zostanie ustanowione między rekordami w różnych bazach danych Entrez, umożliwiając wyszukiwanie powiązanych informacji 	|
|                 	|    **term**    	|               _str_               	| Zapytanie do bazy (np. "viruses[orgn]")                                                                                                           	|
|                 	|   **reldate**  	|               _int_               	| Umożliwia wyszukiwanie rekordów we względnym zakresie dat np. ostatnie X dni od dnia dzisiejszego                                                 	|
|                 	|  **datetype**  	| _str (YYYY/MM/DD, YYYY/MM, YYYY)_ 	| Typ daty do wyszukania (np. "pdat" dla daty publikacji)                                                                                           	|
|                 	|   **mindate**  	| _str (YYYY/MM/DD, YYYY/MM, YYYY)_ 	| Minimalna data wyszukania                                                                                                                         	|
|                 	|   **maxdate**  	| _str (YYYY/MM/DD, YYYY/MM, YYYY)_ 	| Maksymalna data wyszukania                                                                                                                        	|
|                 	|   **retmode**  	|   _`json, enforced by Esearcher_  	| Określa format pobranych danych np.: XML, text, JSON                                                                                              	|
|                 	|    **link**    	|               _bool_              	| Umożliwia wykonywanie zapytań między różnymi bazami danych                                                                                        	|

```python

import entrezpy.elink.elinker

e = entrezpy.elink.elinker.Elinker(tool = "elinker",
                                   email = "zuzwaw5@st.amu.edu.pl",
                                   apikey=None,
                                   apikey_var=None,
                                   threads=None,
                                   qid=None)
analyzer = e.inquire({'dbfrom': 'protein',
                     'db': 'gene',
                     'id': [15718680, 157427902]})

```

## ESUMMARIZER

**entrezpy.esummary.esummarizer.Esummarizer** implementuje narzędzie E-utility ESummary. Esummarizer pobiera podsumowania dokumentów dla identyfikatorów UID w żądanej bazie danych. Podsumowania mogą zawierać streszczenia, szczegóły eksperymentalne, itp.

### Wspierane parametry E-Utility


| **_Narzędzie_** 	| **_Parametr_** 	|            **_Typ_**           	|                                                  **_Opis_**                                                  	|
|:---------------:	|:--------------:	|:------------------------------:	|:------------------------------------------------------------------------------------------------------------:	|
| **Esummarizer**     	|                	|                                	|                                                                                                              	|
|                 	|     **db**     	|              _str_             	| Baza danych do wyszukania (np.: "PubMed", "Protein", "Gene", "Nucleotide")                                   	|
|                 	|     **id**     	|             _list_             	| lista ID używanych do łączenia rekordów w bazach danych Entrez                                               	|
|                 	|   **WebEnv**   	|              _str_             	| połączenie sesji wyszukiwania, umożliwiając żądaniom na dostęp do historii wyszukiwania czy wyników          	|
|                 	|  **retstart**  	|              _int_             	| Określa indeks pierwszego rekordu który ma zostać pobrany umożliwiając pobieranie wyników małymi fragmentami 	|
|                 	|   **retmax**   	|              _int_             	| Określa maksymalną liczbę rekordów pobranych w pojedyńczym żądaniu                                           	|
|                 	|   **retmode**  	| _`json, enforced by Esearcher_ 	| Określa format pobranych danych np.: XML, text, JSON                                                         	|


```python

import entrezpy.esummary.esummarizer

e = entrezpy.esummary.esummarizer.Esummarizer(tool = "esummarizer",
                                              email = "zuzwaw5@st.amu.edu.pl",
                                              apikey=None,
                                              apikey_var=None,
                                              threads=None,
                                              qid=None)

analyzer = e.inquire({'db' : 'pubmed',
                      'id' : [11850928, 11482001]})

print(analyzer.get_result().summaries)

```


## EPOSTER

**entrezpy.epost.eposter.Eposter** implementuje narzędzie E-utility EPost. Eposter wykonuje zapytania, które umieszczają identyfikatory UID na serwerze Historii Entrez i zwracają odpowiadające mu WebEnv i query_key. Jeśli istniejący WebEnv zostanie przekazany jako parametr, dodane zostaną umieszczone UIDs do tego WebEnv poprzez zwiększenie jego query_key.

### Wspierane parametry E-Utility


| **_Narzędzie_** 	| **_Parametr_** 	| **_Typ_** 	|                                              **_Opis_**                                             	|
|:---------------:	|:--------------:	|:---------:	|:---------------------------------------------------------------------------------------------------:	|
| **Eposter**     	|                	|           	|                                                                                                     	|
|                 	|     **db**     	|   _str_   	| Baza danych do wyszukania (np.: "PubMed", "Protein", "Gene", "Nucleotide")                          	|
|                 	|     **id**     	|   _list_  	| lista ID używanych do łączenia rekordów w bazach danych Entrez                                      	|
|                 	|   **WebEnv**   	|   _str_   	| połączenie sesji wyszukiwania, umożliwiając żądaniom na dostęp do historii wyszukiwania czy wyników 	|


```python

import entrezpy.epost.eposter

e = entrezpy.epost.eposter.Eposter(tool = "eposter",
                                   email = "zuzwaw5@st.amu.edu.pl",
                                   apikey=None,
                                   apikey_var=None,
                                   threads=None,
                                   qid=None)

analyzer = e.inquire({'db': 'pubmed',
                      'id': [12466850]})
print(analyzer.get_result().get_link_parameter())

```

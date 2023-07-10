# ENTREZPY TUTORIAL

## Parametry funckji

**apikey** - Ten parametr służy do podania klucza API do uwierzytelniania. Klucz API można uzyskać z usługi bazy danych Entrez i umożliwia on dostęp do niektórych ograniczonych lub uwierzytelnionych funkcji

**apikey_var** - Ten parametr służy do określenia zmiennej środowiskowej zawierającej klucz API.

**threads** - Ten parametr pozwala określić liczbę wątków używanych do wykonywania równoczesnych żądań

**qid** - Ten parametr służy do określania identyfikatora zapytania (QID). QID jest unikalnym identyfikatorem powiązanym z konkretnym zapytaniem lub operacją wyszukiwania.

## INQUIRE()
###inquire() - przyjmuje słownik jako parametr

**db** - Baza danych do wyszukania (np.: "PubMed", "Protein", "Gene", "Nucleotide")

**term** - Zapytanie do bazy (np. "viruses[orgn]")

**retmax** - Maksymalna liczba pobranych rekordów (np. 110000)

**rettype** - Rodzaj rekordów jaki ma być wyodrębniony z bazy (np. "uilist")

**retmode** - Format wyodrębnionych danych (np.: "xml", "text", "json")

**field** - Konkretne pole do wyszukania w bazie danych

**datetype** - Typ daty do wyszukania (np. "pdat" dla daty publikacji)

**mindate** / **maxdate** - Minimalna/Maksymalna data wyszukania

**sort** - Kolejność sortowania

**id** - Określone ID do pobrania (np. lista identyfikatorów UID)

**reldate** - Względny zakres dat do wyszukania (np. "5 dni" dla ostatnich 5 dni).

**usehistory** - Wartość logiczna wskazująca, czy używać serwera historii Entrez.

## ESEARCH

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

## ESUMMARYER

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

## ESPELLER

## EUTILITIES

## EPOST

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

# ENTREZPY TUTORIAL

## Czym jest Entrezpy?

Entrezpy to dedykowana biblioteka w Pythonie do interakcji z bazami danych NCBI poprzez E-Utilities.

## Instalacja

```bash
pip install entrezpy
```

### INQUIRE(parameter, analyzer)

Służy do wysłania zapytania do bazy danych Entrez i pobrania wyników wyszukiwania na podstawie określonych parametrów. Pozwala użytkownikom wyszukiwać rekordy spełniające określone kryteria w bazie danych i uzyskiwać odpowiednie informacje do dalszego przetwarzania lub analizy.
Wykorzystuje dane pobrane za pomocą funkcji zawartej w paczce wykorzystującej E-Utility.

#### **_Parametry:_**
- **parameter (dict)** - Parametry narzędzi E-Utilities
- **analyzer (entrezpy.base.analyzer.EutilsAnalyzer)**

**Zwraca:** analyzer

**Typ zwracany:** entrezpy.base.analyzer.EutilsAnalyzer

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
                'retmax': 1000,
                'rettype': 'uilist'})

print(a.get_result().uids)

```

### Output

```
['2554483202', '2554483201', '2554483200', '2554483199', '2554483198', '2554483197', '2554483196', '2554483195', '2554483194', '2554483193', '2554483192', '2554483191', '2554483190', '2554483189', '2554483188', '2554483187', '2554483186', '2554483185', '2554483184', '2554483183', '2554483182', '2554483181', '2554483180', '2554483179', '2554483178', '2554483177', '2554483176', '2554483175', '2554483174', '2554483173', '2554483172', '2554483171', '2554483170', '2554483169', '2554483168', '2554483167', '2554483166', '2554483165', '2554483164', '2554483163', '2554483162', '2554483161', '2554483160', '2554483159', '2554483158', '2554483157', '2554483156', '2554483155', '2554483154', '2554483153', '2554483152', '2554483151', '2554483150', '2554483149', '2554483148', '2554483147', '2554483146', '2554483145', '2554483144', '2554483143', '2554483142', '2554483141', '2554483140', '2554483139', '2554483138', '2554483137', '2554483136', '2554483135', '2554483134', '2554483133', '2554483132', '2554483131', '2554483130', '2554483129', '2554483128', '2554483127', '2554483126', '2554483125', '2554483124', '2554483123', '2554483122', '2554483121', '2554483120', '2554483119', '2554483118', '2554483117', '2554483116', '2554483115', '2554483114', '2554483113', '2554483112', '2554483111', '2554483110', '2554483109', '2554483108', '2554483107', '2554483106', '2554483105', '2554483104', '2554483103', '2554483102', '2554483101', '2554483100', '2554483099', '2554483098', '2554483097', '2554483096', '2554483095', '2554483094', '2554483093', '2554483092', '2554483091', '2554483090', '2554483089', '2554483088', '2554483087', '2554483086', '2554483085', '2554483084', '2554483083', '2554483082', '2554483081', '2554483080', '2554483079', '2554483078', '2554483077', '2554483076', '2554483075', '2554483074', '2554483073', '2554483072', '2554483071', '2554483070', '2554483069', '2554483068', '2554483067', '2554483066', '2554483065', '2554483064', '2554483063', '2554483062', '2554483061', '2554483060', '2554483059', '2554483058', '2554483057', '2554483056', '2554483055', '2554483054', '2554483053', '2554483052', '2554483051', '2554483050', '2554483049', '2554483048', '2554483047', '2554483046', '2554483045', '2554483044', '2554483043', '2554483042', '2554483041', '2554483040', '2554483039', '2554483038', '2554483037', '2554483036', '2554483035', '2554483034', '2554483033', '2554483032', '2554483031', '2554483030', '2554483029', '2554483028', '2554483027', '2554483026', '2554483025', '2554483024', '2554483023', '2554483022', '2554483021', '2554483020', '2554483019', '2554483018', '2554483017', '2554483016', '2554483015', '2554483014', '2554483013', '2554483012', '2554483011', '2554483010', '2554483009', '2554483008', '2554483007', '2554483006', '2554483005', '2554483004', '2554483003', '2554483002', '2554483001', '2554483000', '2554482999', '2554482998', '2554482997', '2554482996', '2554482995', '2554482994', '2554482993', '2554482992', '2554482991', '2554482990', '2554482989', '2554482988', '2554482987', '2554482986', '2554482985', '2554482984', '2554482983', '2554482982', '2554482981', '2554482980', '2554482979', '2554482978', '2554482977', '2554482976', '2554482975', '2554482974', '2554482973', '2554482972', '2554482971', '2554482970', '2554482969', '2554482968', '2554482967', '2554482966', '2554482965', '2554482964', '2554482963', '2554482962', '2554482961', '2554482960', '2554482959', '2554482958', '2554482957', '2554482956', '2554482955', '2554482954', '2554482953', '2554482952', '2554482951', '2554482950', '2554482949', '2554482948', '2554482947', '2554482946', '2554482945', '2554482944', '2554482943', '2554482942', '2554482941', '2554482940', '2554482939', '2554482938', '2554482937', '2554482936', '2554482935', '2554482934', '2554482933', '2554482932', '2554482931', '2554482930', '2554482929', '2554482928', '2554482927', '2554482926', '2554482925', '2554482924', '2554482923', '2554482922', '2554482921', '2554482920', '2554482919', '2554482918', '2554482917', '2554482916', '2554482915', '2554482914', '2554482913', '2554482912', '2554482911', '2554482910', '2554482909', '2554482908', '2554482907', '2554482906', '2554482905', '2554482904', '2554482903', '2554482902', '2554482901', '2554482900', '2554482899', '2554482898', '2554482897', '2554482896', '2554482895', '2554482894', '2554482893', '2554482892', '2554482891', '2554482890', '2554482889', '2554482888', '2554482887', '2554482886', '2554482885', '2554482884', '2554482883', '2554482882', '2554482881', '2554482880', '2554482879', '2554482878', '2554482877', '2554482876', '2554482875', '2554482874', '2554482873', '2554482872', '2554482871', '2554482870', '2554482869', '2554482868', '2554482867', '2554482866', '2554482865', '2554482864', '2554482863', '2554482862', '2554482861', '2554482860', '2554482859', '2554482858', '2554482857', '2554482856', '2554482855', '2554482854', '2554482853', '2554482852', '2554482851', '2554482850', '2554482849', '2554482848', '2554482847', '2554482846', '2554482845', '2554482844', '2554482843', '2554482842', '2554482841', '2554482840', '2554482839', '2554482838', '2554482837', '2554482836', '2554482835', '2554482834', '2554482833', '2554482832', '2554482831', '2554482830', '2554482829', '2554482828', '2554482827', '2554482826', '2554482825', '2554482824', '2554482823', '2554482822', '2554482821', '2554482820', '2554482819', '2554482818', '2554482817', '2554482816', '2554482815', '2554482814', '2554482813', '2554482812', '2554482811', '2554482810', '2554482809', '2554482808', '2554482807', '2554482806', '2554482805', '2554482804', '2554482803', '2554482802', '2554482801', '2554482800', '2554482799', '2554482798', '2554482797', '2554482796', '2554482795', '2554482794', '2554482793', '2554482792', '2554482791', '2554482790', '2554482789', '2554482788', '2554482787', '2554482786', '2554482785', '2554482784', '2554482783', '2554482782', '2554482781', '2554482780', '2554482779', '2554482778', '2554482777', '2554482776', '2554482775', '2554482774', '2554482773', '2554482772', '2554482771', '2554482770', '2554482769', '2554482768', '2554482767', '2554482766', '2554482765', '2554482764', '2554482763', '2554482762', '2554482761', '2554482760', '2554482759', '2554482758', '2554482757', '2554482756', '2554482755', '2554482754', '2554482753', '2554482752', '2554482751', '2554482750', '2554482749', '2554482748', '2554482747', '2554482746', '2554482745', '2554482744', '2554482743', '2554482742', '2554482741', '2554482740', '2554482739', '2554482738', '2554482737', '2554482736', '2554482735', '2554482734', '2554482733', '2554482732', '2554482731', '2554482730', '2554482729', '2554482728', '2554482727', '2554482726', '2554482725', '2554482724', '2554482723', '2554482722', '2554482721', '2554482720', '2554482719', '2554482718', '2554482717', '2554482716', '2554482715', '2554482714', '2554482713', '2554482712', '2554482711', '2554482710', '2554482709', '2554482708', '2554482707', '2554482706', '2554482705', '2554482704', '2554482703', '2554482702', '2554482701', '2554482700', '2554482699', '2554482698', '2554482697', '2554482696', '2554482695', '2554482694', '2554482693', '2554482692', '2554482691', '2554482690', '2554482689', '2554482688', '2554482687', '2554482686', '2554482685', '2554482684', '2554482683', '2554482682', '2554482681', '2554482680', '2554482679', '2554482678', '2554482677', '2554482676', '2554482675', '2554482674', '2554482673', '2554482672', '2554482671', '2554482670', '2554482669', '2554482668', '2554482667', '2554482666', '2554482665', '2554482664', '2554482663', '2554482662', '2554482661', '2554482660', '2554482659', '2554482658', '2554482657', '2554482656', '2554482655', '2554482654', '2554482653', '2554482652', '2554482651', '2554482650', '2554482649', '2554482648', '2554482647', '2554482646', '2554482645', '2554482644', '2554482643', '2554482642', '2554482641', '2554482640', '2554482639', '2554482638', '2554482637', '2554482636', '2554482635', '2554482634', '2554482633', '2554482632', '2554482631', '2554482630', '2554482629', '2554482628', '2554482627', '2554482626', '2554482625', '2554482624', '2554482623', '2554482622', '2554482621', '2554482620', '2554482619', '2554482618', '2554482617', '2554482616', '2554482615', '2554482614', '2554482613', '2554482612', '2554482611', '2554482610', '2554482609', '2554482608', '2554482607', '2554482606', '2554482605', '2554482604', '2554482603', '2554482602', '2554482601', '2554482600', '2554482599', '2554482598', '2554482597', '2554482596', '2554482595', '2554482594', '2554482593', '2554482592', '2554482591', '2554482590', '2554482589', '2554482588', '2554482587', '2554482586', '2554482585', '2554482584', '2554482583', '2554482582', '2554482581', '2554482580', '2554482579', '2554482578', '2554482577', '2554482576', '2554482575', '2554482574', '2554482573', '2554482572', '2554482571', '2554482570', '2554482569', '2554482568', '2554482567', '2554482566', '2554482565', '2554482564', '2554482563', '2554482562', '2554482561', '2554482560', '2554482559', '2554482558', '2554482557', '2554482556', '2554482555', '2554482554', '2554482553', '2554482552', '2554482551', '2554482550', '2554482549', '2554482548', '2554482547', '2554482546', '2554482545', '2554482544', '2554482543', '2554482542', '2554482541', '2554482540', '2554482539', '2554482538', '2554482537', '2554482536', '2554482535', '2554482534', '2554482533', '2554482532', '2554482531', '2554482530', '2554482529', '2554482528', '2554482527', '2554482526', '2554482525', '2554482524', '2554482523', '2554482522', '2554482521', '2554482520', '2554482519', '2554482518', '2554482517', '2554482516', '2554482515', '2554482514', '2554482513', '2554482512', '2554482511', '2554482510', '2554482509', '2554482508', '2554482507', '2554482506', '2554482505', '2554482504', '2554482503', '2554482502', '2554482501', '2554482500', '2554482499', '2554482498', '2554482497', '2554482496', '2554482495', '2554482494', '2554482493', '2554482492', '2554482491', '2554482490', '2554482489', '2554482488', '2554482487', '2554482486', '2554482485', '2554482484', '2554482483', '2554482482', '2554482481', '2554482480', '2554482479', '2554482478', '2554482477', '2554482476', '2554482475', '2554482474', '2554482473', '2554482472', '2554482471', '2554482470', '2554482469', '2554482468', '2554482467', '2554482466', '2554482465', '2554482464', '2554482463', '2554482462', '2554482461', '2554482460', '2554482459', '2554482458', '2554482457', '2554482456', '2554482455', '2554482454', '2554482453', '2554482452', '2554482451', '2554482450', '2554482449', '2554482448', '2554482447', '2554482446', '2554482445', '2554482444', '2554482443', '2554482442', '2554482441', '2554482440', '2554482439', '2554482438', '2554482437', '2554482436', '2554482435', '2554482434', '2554482433', '2554482432', '2554482431', '2554482430', '2554482429', '2554482428', '2554482427', '2554482426', '2554482425', '2554482424', '2554482423', '2554482422', '2554482421', '2554482420', '2554482419', '2554482418', '2554482417', '2554482416', '2554482415', '2554482414', '2554482413', '2554482412', '2554482411', '2554482410', '2554482409', '2554482408', '2554482407', '2554482406', '2554482405', '2554482404', '2554482403', '2554482402', '2554482401', '2554482400', '2554482399', '2554482398', '2554482397', '2554482396', '2554482395', '2554482394', '2554482393', '2554482392', '2554482391', '2554482390', '2554482389', '2554482388', '2554482387', '2554482386', '2554482385', '2554482384', '2554482383', '2554482382', '2554482381', '2554482380', '2554482379', '2554482378', '2554482377', '2554482376', '2554482375', '2554482374', '2554482373', '2554482372', '2554482371', '2554482370', '2554482369', '2554482368', '2554482367', '2554482366', '2554482365', '2554482364', '2554482363', '2554482362', '2554482361', '2554482360', '2554482359', '2554482358', '2554482357', '2554482356', '2554482355', '2554482354', '2554482353', '2554482352', '2554482351', '2554482350', '2554482349', '2554482348', '2554482347', '2554482346', '2554482345', '2554482344', '2554482343', '2554482342', '2554482341', '2554482340', '2554482339', '2554482338', '2554482337', '2554482336', '2554482335', '2554482334', '2554482333', '2554482332', '2554482331', '2554482330', '2554482329', '2554482328', '2554482327', '2554482326', '2554482325', '2554482324', '2554482323', '2554482322', '2554482321', '2554482320', '2554482319', '2554482318', '2554482317', '2554482316', '2554482315', '2554482314', '2554482313', '2554482312', '2554482311', '2554482310', '2554482309', '2554482308', '2554482307', '2554482306', '2554482305', '2554482304', '2554482303', '2554482302', '2554482301', '2554482300', '2554482299', '2554482298', '2554482297', '2554482296', '2554482295', '2554482294', '2554482293', '2554482292', '2554482291', '2554482290', '2554482289', '2554482288', '2554482287', '2554482286', '2554482285', '2554482284', '2554482283', '2554482282', '2554482281', '2554482280', '2554482279', '2554482278', '2554482277', '2554482276', '2554482275', '2554482274', '2554482273', '2554482272', '2554482271', '2554482270', '2554482269', '2554482268', '2554482267', '2554482266', '2554482265', '2554482264', '2554482263', '2554482262', '2554482261', '2554482260', '2554482259', '2554482258', '2554482257', '2554482256', '2554482255', '2554482254', '2554482253', '2554482252', '2554482251', '2554482250', '2554482249', '2554482248', '2554482247', '2554482246', '2554482245', '2554482244', '2554482243', '2554482242', '2554482241', '2554482240', '2554482239', '2554482238', '2554482237', '2554482236', '2554482235', '2554482234', '2554482233', '2554482232', '2554482231', '2554482230', '2554482229', '2554482228', '2554482227', '2554482226', '2554482225', '2554482224', '2554482223', '2554482222', '2554482221', '2554482220', '2554482219', '2554482218', '2554482217', '2554482216', '2554482215', '2554482214', '2554482213', '2554482212', '2554482211', '2554482210', '2554482209', '2554482208', '2554482207', '2554482206', '2554482205', '2554482204', '2554482203']
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

### Output

```
1. Genome Res. 2007 Mar;17(3):311-9. doi: 10.1101/gr.5823007. Epub 2007 Feb 6.

Sequencing and analysis of chromosome 1 of Eimeria tenella reveals a unique
segmental organization.

Ling KH(1), Rajandream MA, Rivailler P, Ivens A, Yap SJ, Madeira AM, Mungall K,
Billington K, Yee WY, Bankier AT, Carroll F, Durham AM, Peters N, Loo SS, Isa
MN, Novaes J, Quail M, Rosli R, Nor Shamsudin M, Sobreira TJ, Tivey AR, Wai SF,
White S, Wu X, Kerhornou A, Blake D, Mohamed R, Shirley M, Gruber A, Berriman M,
Tomley F, Dear PH, Wan KL.

Author information:
(1)Malaysia Genome Institute, UKM-MTDC Smart Technology Centre, Universiti
Kebangsaan Malaysia, 43600 UKM Bangi, Selangor DE, Malaysia.

Eimeria tenella is an intracellular protozoan parasite that infects the
intestinal tracts of domestic fowl and causes coccidiosis, a serious and
sometimes lethal enteritis. Eimeria falls in the same phylum (Apicomplexa) as
several human and animal parasites such as Cryptosporidium, Toxoplasma, and the
malaria parasite, Plasmodium. Here we report the sequencing and analysis of the
first chromosome of E. tenella, a chromosome believed to carry loci associated
with drug resistance and known to differ between virulent and attenuated strains
of the parasite. The chromosome--which appears to be representative of the
genome--is gene-dense and rich in simple-sequence repeats, many of which appear
to give rise to repetitive amino acid tracts in the predicted proteins. Most
striking is the segmentation of the chromosome into repeat-rich regions peppered
with transposon-like elements and telomere-like repeats, alternating with
repeat-free regions. Predicted genes differ in character between the two types
of segment, and the repeat-rich regions appear to be associated with
strain-to-strain variation.

DOI: 10.1101/gr.5823007
PMCID: PMC1800922
PMID: 17284678 [Indexed for MEDLINE]


2. Biochim Biophys Acta. 1976 Sep 28;446(1):179-91. doi:
10.1016/0005-2795(76)90109-4.

Magnetic studies of Chromatium flavocytochrome C552. A mechanism for heme-flavin
interaction.

Strekas TC.

Electron paramagnetic resonance and magnetic susceptibility studies of
Chromatium flavocytochrome C552 and its diheme flavin-free subunit at
temperatures below 45 degrees K are reported. The results show that in the
intact protein and the subunit the two low-spin (S = 1/2) heme irons are
distinguishable, giving rise to separate EPR signals. In the intact protein
only, one of the heme irons exists in two different low spin environments in the
pH range 5.5 to 10.5, while the other remains in a constant environment. Factors
influencing the variable heme iron environment also influence flavin reactivity,
indicating the existence of a mechanism for heme-flavin interaction.

DOI: 10.1016/0005-2795(76)90109-4
PMID: 9997 [Indexed for MEDLINE]
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

### Output

```

{11850928: {'uid': '11850928', 'pubdate': '1965 Aug', 'epubdate': '', 'source': 'Arch Dermatol', 'authors': [{'name': 'LoPresti PJ', 'authtype': 'Author', 'clusterid': ''}, {'name': 'Hambrick GW Jr', 'authtype': 'Author', 'clusterid': ''}], 'lastauthor': 'Hambrick GW Jr', 'title': 'Zirconium granuloma following treatment of rhus dermatitis.', 'sorttitle': 'zirconium granuloma following treatment of rhus dermatitis', 'volume': '92', 'issue': '2', 'pages': '188-91', 'lang': ['eng'], 'nlmuniqueid': '0372433', 'issn': '0003-987X', 'essn': '', 'pubtype': ['Journal Article'], 'recordstatus': 'PubMed - indexed for MEDLINE', 'pubstatus': '4', 'articleids': [{'idtype': 'pubmed', 'idtypen': 1, 'value': '11850928'}], 'history': [{'pubstatus': 'pubmed', 'date': '1965/08/01 00:00'}, {'pubstatus': 'medline', 'date': '2002/03/09 10:01'}, {'pubstatus': 'entrez', 'date': '1965/08/01 00:00'}], 'references': [], 'attributes': ['Has Abstract'], 'pmcrefcount': '', 'fulljournalname': 'Archives of dermatology', 'elocationid': '', 'doctype': 'citation', 'srccontriblist': [], 'booktitle': '', 'medium': '', 'edition': '', 'publisherlocation': '', 'publishername': '', 'srcdate': '', 'reportnumber': '', 'availablefromurl': '', 'locationlabel': '', 'doccontriblist': [], 'docdate': '', 'bookname': '', 'chapter': '', 'sortpubdate': '1965/08/01 00:00', 'sortfirstauthor': 'LoPresti PJ', 'vernaculartitle': ''}, 11482001: {'uid': '11482001', 'pubdate': '2001 Jun', 'epubdate': '', 'source': 'Adverse Drug React Toxicol Rev', 'authors': [{'name': 'Mantle D', 'authtype': 'Author', 'clusterid': ''}, {'name': 'Gok MA', 'authtype': 'Author', 'clusterid': ''}, {'name': 'Lennard TW', 'authtype': 'Author', 'clusterid': ''}], 'lastauthor': 'Lennard TW', 'title': 'Adverse and beneficial effects of plant extracts on skin and skin disorders.', 'sorttitle': 'adverse and beneficial effects of plant extracts on skin and skin disorders', 'volume': '20', 'issue': '2', 'pages': '89-103', 'lang': ['eng'], 'nlmuniqueid': '9109474', 'issn': '0964-198X', 'essn': '', 'pubtype': ['Journal Article', 'Review'], 'recordstatus': 'PubMed - indexed for MEDLINE', 'pubstatus': '4', 'articleids': [{'idtype': 'pubmed', 'idtypen': 1, 'value': '11482001'}], 'history': [{'pubstatus': 'pubmed', 'date': '2001/08/03 10:00'}, {'pubstatus': 'medline', 'date': '2002/01/23 10:01'}, {'pubstatus': 'entrez', 'date': '2001/08/03 10:00'}], 'references': [], 'attributes': ['Has Abstract'], 'pmcrefcount': '', 'fulljournalname': 'Adverse drug reactions and toxicological reviews', 'elocationid': '', 'doctype': 'citation', 'srccontriblist': [], 'booktitle': '', 'medium': '', 'edition': '', 'publisherlocation': '', 'publishername': '', 'srcdate': '', 'reportnumber': '', 'availablefromurl': '', 'locationlabel': '', 'doccontriblist': [], 'docdate': '', 'bookname': '', 'chapter': '', 'sortpubdate': '2001/06/01 00:00', 'sortfirstauthor': 'Mantle D', 'vernaculartitle': ''}}

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

### Output

```
{'WebEnv': 'MCID_64ca4ee4869cdb6be5451056', 'db': 'pubmed', 'QueryKey': 1}
```

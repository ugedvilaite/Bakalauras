# Karštųjų subnykštukių klasifikavimas taikant funkcinių duomenų analizės metodus

Šioje saugykloje pateikiamas bakalauro baigiamajame darbe naudotas programinis kodas.

**Darbo tema:** Karštųjų subnykštukių klasifikavimas, taikant funkcinių duomenų analizės metodus spektrometriniams duomenims  
**Autorė:** Urtė Gedvilaitė  
**Universitetas:** Vilniaus universitetas, Matematikos ir informatikos fakultetas  
**Metai:** 2026

## Tyrimo tikslas

Darbo tikslas – įvertinti, ar funkcinių duomenų analizės metodai gali būti taikomi Gaia DR3 XP spektrų klasifikavimo uždaviniui, atskiriant dvinares ir nedvinares karštųjų subnykštukių sistemas.

Spektrai nagrinėjami kaip funkciniai duomenys, nes kiekvienas objektas aprašomas srauto reikšmių seka bangos ilgių tinklelyje, t. y. kaip spektrinė kreivė.

## Naudoti metodai

Tyrime taikyti šie metodai:

- pradinė spektrų analizė;
- FPCA ir FPLS;
- atstumu pagrįsti klasifikatoriai;
- k artimiausių kaimynų metodas ir svorinis kNN;
- logistinė regresija;
- tiesinis SVM;
- Gauso glodinimas;
- Vilkoksono ženklų rangų testas;
- modelių interpretuojamumo analizė pagal bangos ilgio sritis.

## Duomenys

Kodas pritaikytas tokiai duomenų katalogo struktūrai:

```text
og_data/
├── xp_sampled_spectra.csv
├── og_xp.csv
└── splits_rskf.json
```

Failų paskirtis:

| Failas | Paskirtis |
|---|---|
| `xp_sampled_spectra.csv` | Diskretizuoti Gaia XP spektrai |
| `og_xp.csv` | Objektų identifikatoriai ir klasės žymės |
| `splits_rskf.json` | Iš anksto sudaryti pakartotinės stratifikuotos kryžminės patikros padalijimai |

Rezultatai išsaugomi `results/` kataloge.

## Saugyklos struktūra

```text
.
├── 00_spectra_visual.ipynb
├── 01_initial_data_exploration.ipynb
├── 02_initial_model_testing.ipynb
├── 03_fpca_vs_fpls.ipynb
├── 04_final_functional_models.ipynb
├── 05_significance_validation.ipynb
├── 06_interpretability.ipynb
├── 07_smoothing.ipynb
└── README.md
```

## Notebook failų aprašas

| Failas | Paskirtis |
|---|---|
| `00_spectra_visual.ipynb` | Sugeneruoja scheminį karštosios subnykštukės ir vėsesnio pagrindinės sekos kompaniono spektrinių indėlių paveikslą. |
| `01_initial_data_exploration.ipynb` | Atlieka pradinę spektrų analizę: skaičiuoja pagrindines charakteristikas, klasių vidurkius, vidurkių skirtumus, koreliacijas ir išvestines. |
| `02_initial_model_testing.ipynb` | Testuoja pradinius atstumu pagrįstus modelius: centroidą, medoidą, kNN ir svorinį kNN su skirtingais atstumais. |
| `03_fpca_vs_fpls.ipynb` | Lygina FPCA ir FPLS reprezentacijas bei jų poveikį klasifikavimo rezultatams. |
| `04_final_functional_models.ipynb` | Sudaro galutinį modelių palyginimą, įtraukiant atstumu pagrįstus modelius, FPCA / FPLS rezultatus ir tiesinius modelius, taikomus tiesiogiai L2 normalizuotiems spektrams. |
| `05_significance_validation.ipynb` | Atlieka atrinktų stipriausių modelių statistinio reikšmingumo analizę naudojant Vilkoksono ženklų rangų testą. |
| `06_interpretability.ipynb` | Atlieka interpretuojamumo analizę: nagrinėja klasių vidurkių skirtumus, FPCA / FPLS projekcijas, atstumo indėlius ir tiesinių modelių svorio funkcijas. |
| `07_smoothing.ipynb` | Vertina Gauso glodinimo poveikį klasifikavimo rezultatams. |

## Modelių vertinimas

Modeliai vertinami naudojant iš anksto sudarytus pakartotinės stratifikuotos kryžminės patikros padalijimus iš failo `splits_rskf.json`.

Tai leidžia:

- visus modelius lyginti tomis pačiomis sąlygomis;
- sumažinti atsitiktinio duomenų padalijimo įtaką;
- atlikti porinius statistinius testus.

Pagrindiniai vertinimo rodikliai:

| Rodiklis | Reikšmė |
|---|---|
| F1 | Harmoninis preciziškumo ir jautrumo vidurkis |
| PR-AUC | Plotas po preciziškumo ir jautrumo kreive |
| ROC-AUC | Plotas po ROC kreive |
| Jautrumas | Teisingai atpažintų dvinarių objektų dalis |
| Specifiškumas | Teisingai atpažintų nedvinarių objektų dalis |
| Preciziškumas | Teisingų dvinarių prognozių dalis |
| Tikslumas | Bendras teisingų prognozių santykis |
| Youdeno J | Jautrumo ir specifiškumo balanso rodiklis |

Pagrindiniais modelių palyginimo rodikliais laikomi F1 ir PR-AUC.


## Programinė aplinka

Analizė atlikta naudojant `Python` ir `Jupyter Notebook`.

Pagrindinės naudotos išorinės bibliotekos:

| Biblioteka | Paskirtis |
|---|---|
| `numpy` | skaitiniai skaičiavimai ir matricų operacijos |
| `pandas` | duomenų nuskaitymas, tvarkymas ir rezultatų lentelės |
| `scikit-learn` | klasifikavimo modeliai, FPKA / FDMKA, kryžminė patikra ir metrikos |
| `scipy` | statistiniai testai, įskaitant Wilcoxono ženklų rangų testą |
| `matplotlib` | grafikų ir paveikslų generavimas |
| `IPython` | tarpinių rezultatų atvaizdavimas notebook aplinkoje |

Papildomai naudotos standartinės `Python` bibliotekos: `json`, `pathlib`, `warnings`, `datetime`, `typing` ir `dataclasses`.

## Paleidimas

1. Patikrinti, ar yra šie failai:

```text
og_data/xp_sampled_spectra.csv
og_data/og_xp.csv
og_data/splits_rskf.json
```

2. Paleisti notebook failus tokia tvarka:

```text
00_spectra_visual.ipynb
01_initial_data_exploration.ipynb
02_initial_model_testing.ipynb
03_fpca_vs_fpls.ipynb
04_final_functional_models.ipynb
05_significance_validation.ipynb
06_interpretability.ipynb
07_smoothing.ipynb
```

3. Rezultatai bus išsaugomi `results/` kataloge.

## Atkuriamumas

Modelių vertinimui naudojami tie patys iš anksto sudaryti kryžminės patikros padalijimai. Kai kuriuose failuose naudojama atsitiktinumo sėkla:

```python
RANDOM_STATE = 42
```

Pagrindinės išvestys:

- `.csv` rezultatų lentelės;
- `.svg` paveikslai, naudoti baigiamajame darbe;
- papildomi `.png` paveikslai peržiūrai.

## Pastaba

Saugykla skirta bakalauro baigiamojo darbo analizės atkuriamumui ir naudoto programinio kodo dokumentavimui.

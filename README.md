# Sistema de diàleg TVD: assistent immobiliari

Dos xatbots que ajuden un usuari a trobar un habitatge (compra o lloguer) a l'àrea de Barcelona. Un funciona amb regles i l'altre amb un LLM i *tools*. Pràctica P1 de l'assignatura Tecnologies de la Veu i el Diàleg (TVD).

## Contingut

| Sistema | Notebook | Dades |
|---|---|---|
| **Basat en regles** | `sistema_regles.ipynb` | `house_data7.json` |
| **Basat en LLM + tools** | `sistema_LLM.ipynb` | `house_data_LLM.json` |

### 1. Assistent basat en regles
Pipeline clàssic de diàleg:
1. Processament de l'entrada (normalització, lèxic, extracció d'atributs).
2. Cerca de pisos sobre el catàleg (26 pisos carregats del JSON).
3. Gestor del diàleg, que decideix quina pregunta fer segons l'ordre de prioritat i les condicions. El pressupost només es pregunta per a compra i els ingressos per a lloguer.
4. Microplanificació i realització de les respostes.
5. Xat interactiu i diàlegs d'exemple.

### 2. Assistent basat en LLM i tools
Utilitza el model **Qwen2.5-Coder-3B-Instruct** (Hugging Face Transformers) amb *function calling*. La millora ve del sistema que envolta el model, no del model:
- Tool `filter_real_estate`, que filtra el catàleg amb el sistema de regles.
- Guardrails d'execució, d'entrada i de sortida.
- Prompt de sistema i bucle de gestió de cada torn.
- Xat interactiu.

## Estructura del repositori

```
.
├── entrega/                 # Lliurament final (notebooks, JSON i informe PDF)
├── notebooks base/          # Notebooks de partida de l'enunciat
├── teoria/                  # Apunts de teoria (PDF)
└── README.md
```

## Requisits

- Python 3.10 o superior
- Jupyter Notebook, JupyterLab o Google Colab
- Només per al sistema LLM: `torch` i `transformers`, més una GPU (provat a Colab amb una Tesla T4)

```bash
pip install jupyter torch transformers accelerate
```

## Com executar-ho

### Sistema basat en regles
1. Obre `entrega/sistema_regles.ipynb`.
2. Deixa `house_data7.json` al mateix directori que el notebook. A Colab, el notebook munta Google Drive i llegeix `/content/drive/MyDrive/TVD/house_data7.json`.
3. Executa totes les cel·les. L'última secció és el xat interactiu.

### Sistema basat en LLM
1. Obre `entrega/sistema_LLM.ipynb`, preferiblement a **Google Colab amb runtime de GPU**.
2. Puja `house_data_LLM.json` quan el notebook ho demani (`files.upload()`).
3. Executa totes les cel·les. La primera vegada es descarrega el model des de Hugging Face.
4. Conversa amb el xat de l'última secció.

## Autores

Berta i Irene

## Llicència

Projecte acadèmic. Afegeix aquí la llicència que vulguis (per exemple MIT).

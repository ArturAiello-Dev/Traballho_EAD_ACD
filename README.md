# 📊 Traballho_EAD_ACD - Monitoramento Automatizado de Tendências em Inteligência Artificial para Desenvolvedores (Devs)

**Desenvolvedores:**  
Artur Aiello, Carolina Navarro, Denis Pereira

Este repositório foi criado para documentar o trabalho desenvolvido pelos discentes Artur Aiello, Carolina Navarro e Denis Pereira, no âmbito da disciplina Extração Automática de Dados, ministrada pelo professor Otávio Xavier, da Universidade Federal de Goiás.

---

## ✨ Descrição do Projeto

Este projeto consiste em um sistema automatizado de web scraping (raspagem de dados da web) para coletar notícias e artigos sobre tendências em Inteligência Artificial Desenvolvedores (Devs). A proposta é manter um monitor de tendências em IA voltadas à Devs, agregando conteúdos de fontes públicas de tecnologia como TecMundo, Canaltech, The Verge, entre outras. Assim, profissionais e interessados podem acompanhar inovações e aplicações de IA no campo, sem precisar buscar manualmente em múltiplos sites. 

A solução realiza a busca de novos conteúdos de forma automatizada a cada semana. Para isso, utiliza Playwright – uma ferramenta moderna de automação de navegador criada pela Microsoft que controla navegadores como Chrome, Firefox e WebKit, permitindo carregar páginas com conteúdo dinâmico (Javascript) como se fosse um usuário real. Em seguida, as páginas são interpretadas com a biblioteca BeautifulSoup (Python) para extrair os dados relevantes de maneira simplificada, sem a necessidade de lidar diretamente com HTML bruto ou expressões regulares. Os dados coletados passam por uma etapa de limpeza e então são analisados para identificar tópicos em destaque, frequência de termos e outras tendências de IA no contexto de SST. Finalmente, um aplicativo web criado com Streamlit apresenta os resultados em um dashboard interativo, com gráficos e listas de notícias filtradas. O Streamlit é um framework Python de código aberto que permite construir aplicativos de dados dinâmicos com poucas linhas de código, ideal para disponibilizar visualizações de forma fácil e acessível diretamente no navegador. 

Em resumo, o sistema cobre todo o fluxo desde a coleta de informações atualizadas sobre IA em SST, passando pelo processamento e análise dos dados, até a visualização dos insights em um dashboard amigável. Tudo isso é feito com foco em ser simples de usar, mesmo para quem tem pouca experiência em programação, bastando seguir as instruções de instalação e execução abaixo.

---

## 📦 Funcionalidades Principais

- **Coleta automática** de notícias e lançamentos de ferramentas de IA de múltiplos sites (Anthropic, TecMundo, Canaltech, The Verge, Gizmodo, AI Directory, etc.).
- **Estrutura de dados organizada** (raw/clean) para facilitar manipulação e atualização.
- **Filtro semântico inteligente**: prioriza notícias realmente relevantes para Devs/IA usando IA de linguagem.
- **Dashboard interativo** (Streamlit): busca por tema, filtro por fonte, ranking de ferramentas, exportação para Excel.
- **Código modular, comentado e fácil de adaptar.**

---

## 🛠️ Tecnologias e Dependências

- **Python 3.10+**
- [BeautifulSoup4](https://www.crummy.com/software/BeautifulSoup/) — parsing HTML
- [Playwright](https://playwright.dev/python/) — scraping de páginas dinâmicas (JS)
- [pandas](https://pandas.pydata.org/) — manipulação de dados
- [streamlit](https://streamlit.io/) — dashboard interativo
- [sentence-transformers](https://www.sbert.net/) — filtro semântico IA
- [openpyxl](https://openpyxl.readthedocs.io/) — exportação Excel

---

### Instalação das dependências

```bash
# Crie e ative o ambiente virtual
python3 -m venv .venv
source .venv/bin/activate    # (Linux/Mac)
# .venv\Scripts\activate     # (Windows)

# Instale as bibliotecas principais
pip install beautifulsoup4 playwright pandas streamlit sentence-transformers openpyxl

# Instale navegadores Playwright (apenas 1 vez!)
playwright install
```
---

### Estrutura das Pastas

```
├── scrape.py                  # Script principal de coleta de notícias/ferramentas
├── app.py                     # Dashboard interativo em Streamlit
├── clean_data/                # Dados limpos prontos para análise
│    └── noticias_YYYY-MM-DD.json
├── raw_data/                  # (opcional) Dados brutos, se quiser guardar o HTML original
├── notebooks/                 # (opcional) Notebooks de análise/experimentos
├── docs/                      # Documentação extra, prints, diagramas
├── requirements.txt           # (opcional) Lista das dependências do projeto
└── README.md
```
---

### Diagrama Resumido do Pipeline
```
+------------------+
|   Múltiplas      |
|     Fontes       | <--- Anthropic, TecMundo, Canaltech, The Verge, etc.
+------------------+
          |
          v
+---------------------+
|   scrape.py         |  # Coleta automatizada (BeautifulSoup/Playwright)
+---------------------+
          |
          v
+---------------------+
|  Limpeza e Filtros  |  # Duplicatas, campos obrigatórios
+---------------------+
          |
          v
+------------------------------+
| clean_data/noticias_YYYY-MM-DD.json |
+------------------------------+
          |
          v
+----------------------+
|    app.py (Streamlit)|
+----------------------+
          |
          v
+----------------------+
| Dashboard Interativo |
+----------------------+
       |        |
       |        +--> Exportação para Excel (.xlsx)
       +--> Busca semântica, filtros, ranking, agrupamento
```
---

### 🚀 Como Executar o Pipeline Completo
Clone este repositório

```bash
git clone <[url-do-repo](https://github.com/ArturAiello-Dev/Traballho_EAD_ACD.git)>
cd <Traballho_EAD_ACD>
(Opcional) Crie e ative um ambiente virtual
```

```bash
python3 -m venv .venv
source .venv/bin/activate      # Linux/Mac
# .venv\Scripts\activate       # Windows
Instale as dependências
```

```bash
pip install -r requirements.txt
# ou manualmente conforme seção anterior
playwright install    # Necessário para scraping de sites dinâmicos!
Execute a coleta de dados
```

```bash
python scrape.py
Isso irá gerar um arquivo JSON em clean_data/ com as notícias/ferramentas mais recentes.
```

Inicie o dashboard

```bash
streamlit run app.py
O dashboard abrirá automaticamente no navegador.
```

### 🧩 Configuração e Personalização
Adicione/remova fontes: edite scrape.py para incluir novos sites/blogs relevantes.

Ajuste filtros semânticos: modifique os parâmetros em app.py para calibrar o nível de relevância.

Troque temas visuais: customize o banner, cores e layout direto no Streamlit.

### 👩‍💻 Execução Recorrente
Para atualizar as notícias semanalmente, execute novamente o scrape.py antes de abrir o dashboard, ou agende uma execução automática com cron (Linux) ou Agendador de Tarefas (Windows).

### ❓ Resolução de Problemas
1) Nenhum dado aparece no dashboard?

Verifique se o arquivo JSON está sendo criado em clean_data/.
Rode python scrape.py e confira as mensagens no terminal (pode haver bloqueios, mudanças de layout dos sites, problemas de conexão).
Veja se as dependências estão corretamente instaladas (pip install ...).

2) Erro ao exportar para Excel?

Instale o pacote: pip install openpyxl

3) Sites sem resultados?

Alguns sites mudam seu layout ou bloqueiam scraping; ajuste os seletores em scrape.py conforme necessário.

### 📄 Licença e Créditos
Todos os direitos das notícias e ferramentas pertencem a seus respectivos autores e sites.

O projeto respeita os termos de uso e políticas das fontes (uso acadêmico, sem redistribuição comercial dos dados coletados).

Desenvolvido por Artur Aiello, Carolina Navarro e Denis Pereira — 2025

### 📚 Referências
BeautifulSoup Documentation

Playwright Python

Streamlit Documentation

Sentence Transformers

---

# Análise de Sentimento em Sentenças Judiciais por Gênero - TJAC

## 📋 Descrição do Projeto

Este projeto investiga se há diferença de sentimento nas sentenças judiciais proferidas por juízes e juízas no Tribunal de Justiça do Acre (TJAC), com foco em processos de **danos morais**. Utilizamos técnicas de web scraping, processamento de linguagem natural (NLP) e análise estatística para responder à pergunta de pesquisa.

**Pergunta de pesquisa:** Há diferença de sentimento na sentença de juízes e juízas no Brasil?

---

## 🎯 Motivação e Escolha do Tema

Escolhemos **danos morais** como tema de pesquisa pelos seguintes motivos:

1. **Alta incidência:** Processos de danos morais são extremamente comuns nos juizados especiais
2. **Subjetividade:** A quantificação de danos morais envolve maior discricionariedade judicial
3. **Relevância social:** Decisões afetam diretamente cidadãos em conflitos cotidianos (consumidor, relações de trabalho, etc.)
4. **Pergunta específica:** Permite investigar se o gênero do julgador influencia o tom/sentimento da decisão

---

## 📁 Estrutura do Projeto

```
projeto-tjac/
│
├── 01_scraping_cnj.ipynb          # Coleta de dados via API DataJud
├── 02_limpeza_htmls.ipynb         # Limpeza e extração de informações
├── 03_classifica_genero.ipynb     # Classificação de gênero dos atores
├── 04_analise_sentimentos.ipynb   # Análise NLP de sentimento e complexidade
├── 05_EDA_Avançado.ipynb          # Análise estatística e visualizações
│
├── requirements.txt               # Dependências do projeto
├── README.md                      # Este arquivo
```

---

## 🚀 Instalação e Execução

### 1. Pré-requisitos

- Python 3.8+
- Jupyter Notebook ou JupyterLab
- Conexão com internet (para scraping)

### 2. Instalação de Dependências

```bash
pip install -r requirements.txt
```

### 3. Ordem de Execução dos Notebooks

**⚠️ IMPORTANTE:** Execute os notebooks na ordem abaixo:

#### **Etapa 1: Coleta de Dados**
```bash
jupyter notebook 01_scraping_cnj.ipynb
```
- **Tempo estimado:** 10-15 minutos
- **Saída:** `processos_tjac_raw.json` (dados brutos da API)

#### **Etapa 2: Limpeza e Extração**
```bash
jupyter notebook 02_limpeza_htmls.ipynb
```
- **Tempo estimado:** 5-10 minutos
- **Entrada:** `processos_tjac_raw.json`
- **Saída:** `processos_tjac_completo.csv` (dados limpos e estruturados)

#### **Etapa 3: Classificação de Gênero**
```bash
jupyter notebook 03_classifica_genero.ipynb
```
- **Tempo estimado:** 2-3 minutos
- **Entrada:** `processos_tjac_completo.csv`, `nomes.csv` (base IBGE + brasileira)
- **Saídas:** 
  - `processos_tjac_com_genero.csv`
  - `dicionario_nomes_classificacao.csv`

#### **Etapa 4: Análise de Sentimentos**
```bash
jupyter notebook 04_analise_sentimentos.ipynb
```
- **Tempo estimado:** 15-20 minutos (processamento NLP)
- **Entrada:** `processos_tjac_com_genero.csv`
- **Saídas:**
  - `processos_tjac_completo_nlp.csv`
  - `processos_tjac_completo_nlp.xlsx`
  - `LEGENDA_NLP.txt`

#### **Etapa 5: Análise Estatística**
```bash
jupyter notebook 05_EDA_Avançado.ipynb
```
- **Tempo estimado:** 5 minutos
- **Entrada:** `processos_tjac_completo_nlp.csv`
- **Saída:** Gráficos e análises estatísticas (exibidos inline)

---

## 📊 Arquivos Gerados

| Arquivo | Descrição | Tamanho Aprox. |
|---------|-----------|----------------|
| `processos_tjac_raw.json` | Dados brutos da API DataJud | ~2 MB |
| `processos_tjac_completo.csv` | Dataset limpo com todas as variáveis | ~500 KB |
| `processos_tjac_com_genero.csv` | Dataset com classificação de gênero | ~600 KB |
| `dicionario_nomes_classificacao.csv` | Dicionário de 100k+ nomes com gênero | ~3 MB |
| `processos_tjac_completo_nlp.csv` | Dataset final com análise NLP | ~700 KB |
| `processos_tjac_completo_nlp.xlsx` | Versão Excel do dataset final | ~800 KB |
| `LEGENDA_NLP.txt` | Documentação das variáveis NLP | 2 KB |

---

## 🔬 Metodologia Resumida

### 1. **Coleta de Dados (Web Scraping)**
- API Pública DataJud/CNJ
- 1200 processos do TJAC (2024-2025)
- Filtro: processos com sentença proferida

### 2. **Limpeza e Extração**
- Parsing de HTML das movimentações
- Extração de: juiz, resultado, partes, advogados
- Taxa de sucesso: 99.9% para identificação de juízes

### 3. **Classificação de Gênero**
- **Método híbrido:** Base IBGE (95% confiança) + Base brasileira 100k nomes (70-90% confiança) + Heurística linguística (60% confiança)
- **Cobertura:** 99.9% dos juízes identificados
- **Confiança média:** 89.8%

### 4. **Análise de Sentimento (NLP)**
- **Sentimento:** Modelo BERT-PT (`lipaoMai/bert-sentiment-model-portuguese`)
- **Complexidade:** Índice Flesch Reading Ease (adaptado para PT)
- **756 sentenças analisadas**

### 5. **Análise Estatística**
- Testes Chi-quadrado
- Testes Mann-Whitney
- Comparações: Gênero × Sentimento × Complexidade × Resultado

---

## 📈 Principais Resultados

- **Sentimento:** 87.6% das sentenças são neutras (esperado em textos jurídicos)
- **Complexidade:** 70.5% alta complexidade (score Flesch médio: 22.8)
- **Gênero dos juízes:** 63.3% feminino vs 36.6% masculino
- **Diferenças estatísticas:** Documentadas no relatório técnico completo

---

## 📝 Documentação Adicional

- **Relatório Técnico:** Ver `RELATORIO_TECNICO.md`
- **Legenda NLP:** Ver `LEGENDA_NLP.txt` (gerado automaticamente)
- **Apresentação:** Slides disponíveis em `apresentacao/`

---

## 👥 Equipe

- **[Seu Nome]** - Análise técnica, implementação, modelagem
- **[Nome do Parceiro]** - Escopo, pesquisa, comunicação

---

## 📚 Referências

- DataJud CNJ: https://www.cnj.jus.br/sistemas/datajud/
- BERT-PT: https://huggingface.co/lipaoMai/bert-sentiment-model-portuguese
- Flesch Reading Ease: Flesch, R. (1948)
- Base de Nomes IBGE: Instituto Brasileiro de Geografia e Estatística

---

## ⚖️ Ética e Conformidade

- ✅ Dados públicos (processos judiciais)
- ✅ Anonimização de nomes completos
- ✅ Transparência sobre erros e incertezas
- ✅ Código reproduzível e versionado
- ✅ Conformidade com LGPD

---

## 📧 Contato

Para dúvidas ou sugestões sobre este projeto:
- Email: [seu-email@exemplo.com]
- GitHub: [link-do-repositorio]

---

## 📄 Licença

Este projeto é desenvolvido para fins acadêmicos (Mestrado em Machine Learning).

---

**Última atualização:** Dezembro 2024

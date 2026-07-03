# 🎙️ Challenge FIAP & TOTVS - Assistente de Voz e Transcrição Inteligente

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![OpenAI Whisper](https://img.shields.io/badge/OpenAI_Whisper-412991?style=for-the-badge&logo=openai&logoColor=white)

## 📌 Introdução

Este projeto foi desenvolvido como parte do **Enterprise Challenge**, uma atividade extensionista do curso de **Tecnologia em Data Science, Big Data, BI & Data Engineering** da **FIAP**. 

O objetivo principal do Challenge é simular a experiência profissional do mercado de trabalho através de uma metodologia hands-on, aplicando técnicas, ferramentas e boas práticas acadêmicas para propor soluções reais a desafios demandados por empresas parceiras. Nesta edição, o projeto foi construído em parceria com a **TOTVS**, uma das maiores empresas de tecnologia do mundo e líder no mercado de Software de Gestão Empresarial (ERP) no Brasil.

## 🚀 O Desafio Proposto

A TOTVS realiza pesquisas de **NPS (Net Promoter Score)** com seus clientes. Para os clientes classificados como detratores (aqueles com experiências negativas), a empresa realiza um diagnóstico interno para direcionar os problemas às áreas responsáveis pelas resoluções. 

### Cenário Atual e Problemática
Atualmente, o processo de transcrição das ligações de suporte e pesquisas possui baixa qualidade. Essa perda de fidelidade nos textos ocorre devido a:

* Ruídos nos áudios das gravações.
* Variedade de sotaques e uso de gírias por parte dos clientes.
* Pouco suporte nativo das ferramentas atuais para o idioma português.

Como a empresa processa uma média de **80 ligações por dia**, o tempo e o custo operacional tornam-se fatores críticos para o negócio.

### O Objetivo do Projeto
O desafio consiste em desenvolver um sistema eficiente de transcrição de áudios de ligações sobre a pesquisa de NPS. A solução deve focar em:

1. **Alta Qualidade de Transcrição:** Garantir precisão na conversão de áudio para texto, superando as barreiras de ruídos e sotaques regionais.
2. **Processamento de Linguagem Natural (NLP):** Aplicar técnicas de NLP para extrair insights valiosos dos textos transcritos.
3. **Análise de Sentimentos e Classificação:** Automatizar o diagnóstico mapeando os macro motivos das insatisfações e medindo a "temperatura" da pressão dos clientes para priorização de ações internas da TOTVS.
4. **Eficiência de Custo:** Priorizar o uso de ferramentas e bibliotecas open-source para viabilizar o processamento em lotes dentro do volume diário da companhia.

## 🛠️ Solução Desenvolvida & Arquitetura Técnica

Para solucionar o problema de baixa qualidade de transcrição e viabilizar a eficiência de custo exigida, desenvolvemos um pipeline em Python focado em inteligência de áudio.

### 1. Transcrição com OpenAI Whisper (Open-Source)
Como o volume é de 80 ligações/dia, optou-se pela utilização do **Whisper**, modelo da OpenAI que roda de forma open-source. No notebook, realizamos um benchmark avaliando diferentes capacidades do modelo utilizando um áudio de NPS real da TOTVS como caso de teste:

* **Modelo small:** Mais leve e rápido, porém propenso a entrar em loops de repetição em trechos com silêncio ou ruído.
* **Modelos medium e large:** Apresentaram performance excepcional, superando as barreiras de ruídos da linha e sotaques. Conseguiram capturar com precisão nomes de filiais (ex: Uberlândia, Rio Preto), dados sensíveis (CNPJ, e-mails) e as notas atribuídas a cada setor avaliado na pesquisa.

### 2. O Fluxo de Inteligência de Dados
A transcrição é apenas o primeiro passo. A inteligência da nossa solução funciona como uma esteira automatizada:

1. **Tratamento de Áudio:** O ffmpeg faz a leitura e a limpeza prévia do arquivo de som.
2. **Speech-to-Text:** O Whisper extrai o texto fiel da chamada, resolvendo o problema de perda de qualidade.
3. **Extração de KPIs via Regex:** Utilizamos expressões regulares no Python para buscar de forma automatizada e estruturada as notas (0 a 10) de setores específicos como Atendimento Comercial, Financeiro e Agilidade.
4. **Análise de Sentimento e Classificação (NLP):** O texto limpo é alimentado na API da OpenAI (ChatGPT) para ler a conversa e identificar o nível de urgência do cliente detrator, mapeando automaticamente o "macro motivo" da insatisfação.
5. **Cenários de Retorno por Voz:** Deixamos a estrutura integrada à API da ElevenLabs para que o sistema possa, no futuro, gerar alertas falados ou interagir de volta utilizando síntese de voz ultrarrealista.

### 3. Dashboard de Monitoramento (NPS & Sentimentos)
Para que a diretoria e os gestores da TOTVS consigam visualizar os resultados em tempo real, integramos os dados extraídos pelo nosso pipeline a um dashboard analítico. Ele consolida o volume de gravações processadas, a distribuição de sentimentos e as médias de avaliação por setor, facilitando a tomada de decisão rápida sobre os clientes detratores:

![Dashboard Indata](images/image_3b05a7.png)

## 💻 Tecnologias Utilizadas

* **Processamento de Áudio:** librosa, soundfile, ffmpeg-python
* **Machine Learning & NLP:** openai-whisper, openai (API), tensorflow, keras
* **Engenharia e Estruturação de Dados:** pandas, numpy, re (Regex)
* **Visualização Analítica:** matplotlib, seaborn

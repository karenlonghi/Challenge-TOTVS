# Challenge FIAP & TOTVS — Assistente de Voz e Transcrição Inteligente

## 📌 Introdução
Este projeto foi desenvolvido como parte do **Enterprise Challenge**, uma atividade extensionista do curso de **Tecnologia em Data Science, Big Data, BI & Data Engineering** da **FIAP**. 

O objetivo principal do Challenge é simular a experiência profissional do mercado de trabalho através de uma metodologia hands-on, aplicando técnicas, ferramentas e boas práticas acadêmicas para propor soluções reais a desafios demandados por empresas parceiras. Nesta edição, o projeto foi construído em parceria com a **TOTVS**, uma das maiores empresas de tecnologia do mundo e líder no mercado de Software de Gestão Empresarial (ERP) no Brasil.

---

## 🚀 O Desafio Proposto
A TOTVS realiza pesquisas de **NPS (Net Promoter Score)** com seus clientes. Para os clientes classificados como detratores (aqueles com experiências negativas), a empresa realiza um diagnóstico interno para direcionar os problemas às áreas responsáveis pelas resoluções. 

### Cenário Atual e Problemática
Atualmente, o processo de transcrição das ligações de suporte e pesquisas possui baixa qualidade. Essa perda de fidelidade nos textos ocorre devido a:
* Ruídos nos áudios das gravações;
* Variedade de sotaques e uso de gírias por parte dos clientes;
* Pouco suporte nativo das ferramentas atuais para o idioma português.

Como a empresa processa uma média de **80 ligações por dia**, o tempo e o custo operacional tornam-se fatores críticos para o negócio.

### O Objetivo do Projeto
O desafio do grupo consiste em desenvolver um sistema eficiente de transcrição de áudios de ligações sobre a pesquisa de NPS. A solução deve focar em:
1. **Alta Qualidade de Transcrição:** Garantir precisão na conversão de áudio para texto, superando as barreiras de ruídos e sotaques regionais.
2. **Processamento de Linguagem Natural (NLP):** Aplicar técnicas de NLP para extrair *insights* valiosos dos textos transcritos.
3. **Análise de Sentimentos e Classificação:** Automatizar o diagnóstico mapeando os macro motivos das insatisfações e medindo a "temperatura" da pressão dos clientes para priorização de ações internas da TOTVS.
4. **Eficiência de Custo:** Priorizar o uso de ferramentas e bibliotecas open-source para viabilizar o processamento em lotes dentro do volume diário da companhia.

---

## 🛠️ Solução Desenvolvida & Arquitetura Técnica

Para solucionar o problema de baixa qualidade de transcrição e viabilizar a eficiência de custo exigida, o grupo desenvolveu um pipeline em Python focado em inteligência de áudio:

### 1. Transcrição com OpenAI Whisper (Open-Source)
Como o volume é de 80 ligações/dia, optou-se pela utilização do **Whisper**, o modelo estado-da-arte em reconhecimento de fala da OpenAI que roda de forma open-source. No notebook, o grupo realizou um benchmark avaliando diferentes capacidades do modelo utilizando um áudio de NPS real da TOTVS como caso de teste:
* **Modelo small:** Mais leve e rápido, porém propenso a entrar em loops de repetição em trechos com silêncio ou ruído.
* **Modelo medium e large:** Apresentaram performance excepcional, superando as barreiras de ruídos da linha e sotaques. Conseguiram capturar com precisão nomes de filiais (ex: Uberlândia, Rio Preto), dados sensíveis (CNPJ, e-mails) e as notas atribuídas a cada setor avaliado na pesquisa.

### 2. Preparação para Processamento Cognitivo e Síntese (NLP & TTS)
Além da transcrição (Speech-to-Text), o ambiente do projeto foi preparado com as fundações necessárias para a automação completa do diagnóstico:
* **ffmpeg-python:** Para a manipulação, limpeza e leitura ágil dos formatos de áudio do sistema.
* **API OpenAI (ChatGPT):** Integrada para a camada de Processamento de Linguagem Natural (NLP), viabilizando a extração automática de macro motivos, resumos estruturados e análise de sentimento/temperatura do cliente.
* **API ElevenLabs:** Estruturada para cenários onde a TOTVS necessite de respostas e interações via síntese de voz ultra-realista por IA (Text-to-Speech).

---

## 💻 Como Executar o Projeto

### Pré-requisitos
Certifique-se de ter o ffmpeg instalado no seu sistema operacional (necessário para o processamento de áudio por trás das bibliotecas).

### Instalação das Dependências
Execute os comandos abaixo para instalar as bibliotecas configuradas no ecossistema do projeto:

```bash
pip install ffmpeg-python openai elevenlabs
pip install git+[https://github.com/openai/whisper.git](https://github.com/openai/whisper.git)

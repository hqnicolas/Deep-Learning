# Projeto Integrador: Deep Learning


## 1. O que é um Projeto Integrador?
* Um **Projeto Integrador (PI)** é uma atividade curricular que visa integrar os conhecimentos adquiridos em diferentes disciplinas de um curso universitário.
* O objetivo é aplicar esses conhecimentos na prática, de forma interdisciplinar, para solucionar um problema real da comunidade ou do mercado de trabalho.

### Características de um Projeto Integrador
* **Abordagem Interdisciplinar:** Combina conhecimentos de diferentes áreas do saber.
* **Resolução de Problemas:** Envolve a aplicação prática dos conhecimentos para solucionar problemas reais.
* **Autonomia dos Alunos:** Estimula a autonomia, a criatividade e o trabalho em equipe.
* **Orientação Docente:** Conta com a orientação de um professor.
* **Avaliação Contínua:** O processo de aprendizagem é avaliado de forma contínua.

---

## 2. Benefícios de um Projeto Integrador
* **Desenvolvimento de Habilidades:** Estimula o desenvolvimento de habilidades como pesquisa, comunicação, trabalho em equipe, resolução de problemas e pensamento crítico.
* **Preparação para o Mercado de Trabalho:** Aproxima os alunos da realidade profissional e os prepara para os desafios do mercado de trabalho.
* **Impacto Social:** Promove a aplicação dos conhecimentos para o desenvolvimento da comunidade e da sociedade.

---

## 3. O que é Projeto de Extensão?
* Projetos de Extensão são atividades que conectam a universidade à comunidade externa, promovendo a interação e o desenvolvimento mútuo.
* Através da Extensão, o conhecimento acadêmico é aplicado na prática, buscando soluções para problemas reais e impactando positivamente a vida das pessoas.

### Benefícios dos Projetos de Extensão
* **Para a comunidade:** Acesso a conhecimento e serviços, desenvolvimento de habilidades, empoderamento, resolução de problemas.
* **Para os alunos:** Experiência prática, contato com diferentes realidades, desenvolvimento de habilidades e enriquecimento curricular.
* **Para a universidade:** Integração com a comunidade, fortalecimento da responsabilidade social, aprimoramento da formação dos alunos.

---

## 4. Exemplos Práticos de Visão Computacional

### 4.1. Detecção de Lixos
* Utilização de redes profundas para identificação e classificação de resíduos/embalagens em imagens (ex: *Packaged goods*, garrafas, latas).

<img width="995" height="664" alt="image" src="https://github.com/user-attachments/assets/2862949d-2e6e-4feb-824a-5e9c201ab814" />

  
* **Referência:** [Computer Vision for Garbage Detection (Medium)](https://medium.com/ramudroid/computer-vision-for-garbage-detection-136029142b3c)

### 4.2. Detecção de Animais
* Identificação de faces e raças de animais de estimação (`dogFace`).

<img width="683" height="679" alt="image" src="https://github.com/user-attachments/assets/d35338d3-2114-4b51-98ae-67e92749f1df" />

  
* **Referência:** [Deep Learning: Recognise Your Home Pets (Towards Data Science)](https://towardsdatascience.com/deep-learning-recognise-your-home-pets-82a35d524703)

### 4.3. Detecção de Fadiga em Motoristas
* Monitoramento visual em tempo real para detecção de olhos fechados (sonolência) ou distração (uso de celular ao volante).

<img width="908" height="510" alt="image" src="https://github.com/user-attachments/assets/bff79235-01b3-4f8d-bd20-d23da8671cd5" />


* **Referência:** [Driver Drowsiness Detection System (DataFlair)](https://data-flair.training/blogs/python-project-driver-drowsiness-detection-system/)

---

## 5. Large Language Models (LLMs)
* LLMs são modelos gigantescos e extremamente pesados, sendo de difícil treinamento sem uma infraestrutura adequada.
* Podemos usar modelos prontos localmente ou através de APIs (ex: **Ollama**).
* São excelentes para diversas tarefas e permitem criar pipelines de resolução de problemas.
* **Limitação:** Os dados a que o modelo tem acesso restringem-se apenas àqueles contidos no seu treinamento original.
* **Solução:** Para buscar dados de outras fontes, precisamos de um mecanismo para resgatar essas informações e fornecê-las como contexto para o modelo.

---

## 6. RAG (Retrieval-Augmented Generation)

<img width="613" height="466" alt="image" src="https://github.com/user-attachments/assets/7f75ae75-1a77-44e5-a13f-705b4760bf04" />

### 6.1. Conceito Central
* A ideia do RAG é buscar informações relevantes em uma base de documentos e repassá-las como contexto para a LLM.
* **Analogia:** 
  * Se perguntarmos a um aluno *"Em que ano ocorreu a Revolução Francesa?"* sem que ele tenha estudado o assunto, ele pode errar.
  * Se disponibilizarmos livros de história para ele consultar antes de responder, ele encontrará a resposta correta.
* **Fluxo simplificado:**
  $$	ext{Query} \longrightarrow 	ext{Knowledge Base} \longrightarrow 	ext{Relevant Context} \longrightarrow 	ext{LLM} \longrightarrow 	ext{Response}$$

### 6.2. Knowledge Base e Banco de Dados Vetorial
* O conhecimento a ser fornecido para a rede é armazenado em um **Banco de Dados Vetorial (Vector DB)**.
* Ao criar essa base, os documentos passam pelo mesmo modelo de *Embedding/Encoder* da LLM para salvar seus vetores representativos.
* **Pipeline de Ingestão:** `Load` $\longrightarrow$ `Split` $\longrightarrow$ `Embed` $\longrightarrow$ `Store`

### 6.3. Chunking e Contexto
* Como toda LLM possui uma **janela de contexto de tamanho fixo**, documentos grandes são divididos em pequenos trechos (*chunks*).
* A tarefa final do RAG é buscar o *chunk* que possui a maior similaridade semântica com o *prompt* do usuário.
* Calculam-se distâncias vetoriais (Cosseno, Manhattan, Euclidiana, etc.) para identificar os $n$ *chunks* mais próximos.
* **Prompt montado:**
  * **Input:** *"Em que ano ocorreu..."*
  * **Contexto enviado:** `chunk_1, chunk_2, ..., chunk_n`

### 6.4. Arquiteturas e Evolução do RAG
* **Componentes de Produção:** Vector DBs (Redis, Elasticsearch, Cassandra) + LLMs (OpenAI, Mistral AI, Anthropic).
* **Melhorias e Variações Avançadas:**
  * Uso de **Multi-Agentes** para classificar e validar se o contexto recuperado faz sentido.
  * **Busca na Internet** como *fallback* caso a informação não esteja no banco interno.
  * Comparativo de abordagens: *Naive RAG*, *Advanced RAG* e *Modular RAG* (técnicas como DSP, ITER-RETGEN, *Query Rewriting*, *Rerank*, *Fusion*).

---

## 7. Aplicações Práticas com LLMs
Ao desenvolver aplicações baseadas em LLM, deve-se considerar:
* **Comunicação Modelo $\leftrightarrow$ Aplicação:** Integração fluida via API ou local.
* **Avaliação do Modelo:** Métricas e validação de qualidade das respostas.
* **Segurança:** Uso de *Guard-Rails*, proteção contra *prompt injection* / ataques e mitigações contra alucinações.
* **Integrações:** Uso de APIs gratuitas e modelos Open Source.
* **Referência:** [Top Free LLM Tools, APIs & Open Source Models (Eden AI)](https://www.edenai.co/post/top-free-llm-tools-apis-and-open-source-models)
transcricao_aula_1.md
Displaying transcricao_aula_1.md.

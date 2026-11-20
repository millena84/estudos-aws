# AWS Certified AI Practitioner (AIF-C01) — guia de estudo

Referência: 20/11/2026. Documento em português para importação no NotebookLM.

## 1. Escopo, fontes e como estudar

Este material cobre os 14 objetivos dos cinco domínios publicados e as 51 entradas do catálogo oficial, nas mesmas 11 categorias. A AWS informa que o guia não é exaustivo e pode mudar: “todos” aqui significa todos os objetivos e serviços explicitamente publicados, não garantia de prever todas as questões. Algumas entradas são ferramentas ou famílias, não serviços faturados de forma independente. As funcionalidades e pegadinhas são explicações para estudo, não questões vazadas nem previsão de frequência.

A referência [G] indica o guia geral; [D1] a [D5], os domínios; [CAT], a classificação oficial; [P] indica páginas de preços e produto. Todos os links ficam na seção final para facilitar uso como fontes no NotebookLM. Conteúdo complementar é identificado quando não é uma entrada/menção independente do programa. A cobrança é descrita por unidades, não por tabela de valores: Região, edição, modelo, modalidade, descontos e recursos associados afetam custo e disponibilidade.

### Formato da prova [G]

- 65 questões: 50 pontuadas e 15 experimentais não identificadas.
- Questões de escolha única e múltiplas respostas.
- Nota em escala 100–1.000; aprovação a partir de 700. Isso não equivale necessariamente a 70% de acertos.
- Questão não respondida conta como incorreta; não há penalidade adicional por tentativa.
- Não é necessário passar isoladamente em cada domínio: vale o desempenho global ponderado.
- O nível é de fundamentos e aplicação de negócio: não exige programar modelos, implementar engenharia de dados/features, executar tuning, construir pipelines/infraestrutura, realizar análises matemáticas avançadas nem implementar protocolos e frameworks de governança. Saber explicar e escolher essas atividades continua relevante.

| Domínio | Peso |
|---|---:|
| 1 — Fundamentos de IA e ML | 20% |
| 2 — Fundamentos de GenAI | 24% |
| 3 — Aplicações de modelos fundacionais | 28% |
| 4 — Diretrizes de IA responsável | 14% |
| 5 — Segurança, conformidade e governança | 14% |

## 2. Conteúdo por domínio e objetivo

### Domínio 1 — Fundamentos de IA e ML [D1]

#### 1.1 Conceitos básicos e terminologia

IA é o campo amplo de sistemas que realizam tarefas associadas à inteligência. ML aprende padrões a partir de exemplos, em vez de programar cada regra. Deep learning é ML com redes neurais de múltiplas camadas. GenAI gera novos conteúdos a partir de padrões aprendidos. LLM é modelo de linguagem de grande escala; IA agêntica combina modelo, ferramentas, memória e decisões para perseguir um objetivo. Um detector de fraude pode ser ML sem gerar conteúdo; nem toda aplicação de IA precisa de agente.

- Algoritmo é o método de aprendizado; modelo é o resultado parametrizado. Rede neural combina camadas de unidades com parâmetros ajustáveis.
- Treinamento ajusta parâmetros; inferência usa o modelo para prever/gerar. Hiperparâmetros orientam o treino, como taxa de aprendizado ou épocas, e não são a mesma coisa que pesos aprendidos.
- Inferência batch processa conjuntos sem resposta imediata; tempo real atende requisições síncronas; assíncrona aceita requisição e entrega depois; serverless descreve o gerenciamento de capacidade. Serverless não é sinônimo de batch nem de ausência de limites.
- Dados rotulados têm alvo conhecido; não rotulados não. Tabulares seguem colunas; séries temporais dependem de ordem temporal; imagens/textos são usualmente não estruturados; JSON é exemplo semiestruturado.
- Supervisionado: classificação prevê categoria, regressão prevê número. Não supervisionado: clustering encontra grupos. Reforço: aprende política por interação e recompensa, não simplesmente por ler uma instrução.
- Visão computacional interpreta imagens/vídeos; NLP processa linguagem; reconhecimento de fala converte áudio em texto.
- Fit é ajuste aos padrões; viés pode ser simplificação estatística ou desigualdade sistemática entre grupos. Fairness trata critérios de equidade, não é sinônimo de accuracy.

Analogia: algoritmo é o método de estudo; dados são exercícios; treinamento é estudar; modelo é a competência adquirida; inferência é resolver uma questão nova. Decorar o gabarito sem generalizar é overfitting.

#### 1.2 Casos de uso e escolha da abordagem

| Necessidade | Abordagem típica | Cuidado |
|---|---|---|
| Fraude ou legítima | Classificação supervisionada | Avaliar falsos negativos e falsos positivos |
| Estimar valor de compra | Regressão | Saída numérica, não rótulo |
| Segmentar clientes por comportamento | Clustering | Grupo descoberto não é diagnóstico verdadeiro |
| Prever demanda futura | Previsão/séries temporais | Não usar informação futura no treino |
| Selecionar produtos para cada usuário | Recomendação, por exemplo Personalize | Gerar descrição com LLM não substitui ranking |
| Resumir e redigir conteúdo | Modelo generativo | Conferir factualidade e confidencialidade |
| Responder sobre política atual com fontes | RAG | Recuperação precisa respeitar autorização |
| Consultar e agir em sistemas | Agente com ferramentas limitadas | Ação precisa de permissão e validação |
| Aplicar exatamente regra de tarifa | Código/regra determinística | Predição probabilística pode ser desnecessária |

Avalie custo-benefício, necessidade real de previsão, disponibilidade e qualidade dos dados, risco, explicabilidade, requisitos regulatórios, operação e latência. ML tradicional pode ser mais adequado a score tabular; FM pode ser melhor para linguagem e documentos. APIs gerenciadas como Transcribe, Translate, Comprehend, Lex e Polly evitam construir um modelo para tarefas prontas.

#### 1.3 Ciclo de desenvolvimento e MLOps

1. Definir problema, métricas técnicas/de negócio e baseline.
2. Coletar dados com proveniência, direitos de uso e controles.
3. Limpar, rotular e transformar; separar treino, validação e teste.
4. Selecionar algoritmo, modelo pré-treinado aberto/licenciado ou modelo próprio.
5. Treinar/adaptar e comparar experimentos usando validação.
6. Avaliar em teste independente, subgrupos e casos adversos.
7. Implantar via API gerenciada ou hospedagem própria; selecionar modo de inferência.
8. Monitorar qualidade, latência, custo, segurança e feedback; retreinar/reavaliar quando necessário.

Treino aprende; validação orienta escolhas; teste mede generalização final. Vazamento de dados ocorre quando treino/avaliação usa informações indisponíveis no cenário real. Data drift muda distribuição das entradas; concept drift muda relação entre entrada e resultado. Retreino não deve ser automático sem avaliação.

MLOps organiza experimentação, repetição, escalabilidade, dívida técnica, prontidão de produção, rastreabilidade, monitoramento e retreino. S3 guarda dados; Glue/EMR preparam; SageMaker AI treina/implanta; Bedrock oferece FMs; Quick apoia análise e produtividade conforme componente; Kiro auxilia desenvolvimento. Versionar código, dados, prompts e modelos facilita comparação e auditoria.

### Domínio 2 — Fundamentos de IA generativa [D2]

#### 2.1 Conceitos, ciclo do FM e IA agêntica

- FM é modelo pré-treinado em dados amplos e reutilizável em tarefas; LLM é um tipo de FM, não toda a categoria.
- Token é unidade de representação processada pelo modelo; pode ser parte de palavra. Palavra, caractere e token não são equivalentes.
- Transformer usa mecanismos de atenção para relacionar elementos da sequência. Difusão é uma abordagem generativa relacionada à remoção gradual de ruído, comum em geração de imagem; não é a arquitetura de todo modelo.
- Modelo multimodal aceita/produz modalidades como texto, imagem e áudio conforme capacidades específicas; aceitar imagem não significa gerar imagem.
- Chunking divide documentos em blocos; overlap preserva continuidade entre blocos adjacentes. Bloco muito pequeno perde contexto; muito grande aumenta ruído/tokens.
- Embedding é representação numérica de significado; vetor é uma sequência de valores. Busca vetorial recupera por proximidade semântica. Não é criptografia, anonimização ou uma resposta final por si só.
- Prompt engineering organiza instruções e exemplos; context engineering organiza todo o contexto relevante: histórico, documentos recuperados, ferramentas, memória e limites.
- Janela de contexto limita o conteúdo processado na interação conforme modelo/API. Não é memória durável nem atualização dos pesos. Histórico reenviado e documentos podem ocupar tokens.
- Ciclo de FM: selecionar dados e modelo → pré-treinar quando necessário → adaptar/fine-tuning → avaliar → implantar → coletar feedback. Consumir FM existente evita custo de pré-treino do zero.

Usos: geração de imagem/vídeo/áudio, resumo, tradução, busca, assistentes, código, atendimento e recomendação com técnicas apropriadas. IA agêntica envolve ciclo de decisão, ferramenta, observação e próximo passo; multiagentes podem ter supervisor/especialistas, encaminhamento ou colaboração. Mais agentes podem elevar latência, custo e risco.

MCP (Model Context Protocol) padroniza conexão com ferramentas/fontes externas; não é um modelo nem concede autorização. Memória de curto prazo atende sessão/contexto; longo prazo persiste informações conforme política. Workflow orquestrado pode ser determinístico; não é obrigatório deixar todas as decisões com o modelo.

#### 2.2 Capacidades, limitações e valor

Vantagens: adaptação, conversação, resposta a diferentes tarefas e geração de conteúdo. Limitações: alucinações, inexatidão, não determinismo e interpretabilidade. Texto convincente não é evidência de verdade; reduzir temperatura não elimina erro factual.

Seleção exige tarefa/modalidade, idioma, qualidade medida, latência, custo, complexidade, restrições, compliance e operação. Modelo maior não é automaticamente melhor. Métricas de valor incluem ROI, produtividade, eficiência, conversão, receita média por usuário, valor vitalício, engajamento e satisfação. Avalie tarefas reais, não apenas benchmark genérico ou “parece inteligente”.

#### 2.3 Tecnologias AWS e infraestrutura

Bedrock: consumo de FMs e recursos de aplicação. SageMaker AI: desenvolver, treinar, adaptar e hospedar com mais controle. JumpStart: modelos e soluções iniciais. Quick: analytics/produtividade conforme componente. Kiro: desenvolvimento assistido. Strands Agents: SDK de agentes. AgentCore: componentes gerenciados para operação de agentes.

Serviços gerenciados facilitam acesso, reduzem barreiras e aceleram entrega, mas cliente mantém responsabilidades por dados, permissões, aplicação, avaliação e uso. Mais disponibilidade, redundância, baixa latência e capacidade provisionada podem aumentar custo. Região afeta disponibilidade, residência e preço. Modelos customizados podem trazer treino, armazenamento e inferência próprios.

### Domínio 3 — Aplicações de modelos fundacionais [D3]

#### 3.1 Seleção, RAG, parâmetros, customização e agentes

Compare custo, modalidade, idioma, latência, complexidade/tamanho, limite de entrada/saída, adaptação e cache de prompt. Temperatura regula aleatoriedade na amostragem, quando suportada. Top-k/top-p são controles complementares em modelos que os oferecem (aprofundamento); não são controles de verdade. Limitar saída economiza, mas pode truncar; contexto maior acomoda fontes e pode elevar ruído/custo.

RAG combina recuperação externa e geração. Fluxo típico: fonte autorizada → limpeza → chunks → embeddings → índice → pergunta → busca → reranking opcional → contexto → geração → validação/citações. Knowledge Bases automatiza partes. RAG por si só não altera pesos, não elimina alucinações e não garante autorização de cada documento.

O guia cita OpenSearch, Aurora, Neptune e RDS for PostgreSQL para embeddings/bancos vetoriais. A funcionalidade depende de produto, engine, versão e extensões: pgvector em PostgreSQL e capacidades de Neptune Analytics não significam suporte igual em toda edição. Atualizar documento pode exigir atualizar índice; remover fonte não garante remoção imediata de cópias/chunks/cache.

| Abordagem | Altera pesos? | Quando é boa opção | Limitação/custo |
|---|---|---|---|
| Prompt / in-context learning | Não | Instruções e exemplos para tarefa | Tokens e limite de contexto |
| RAG | Não, por si só | Conteúdo externo atual e citável | Ingestão, índice, recuperação e geração |
| Fine-tuning | Sim | Estilo, comportamento e tarefa especializada | Dados curados, treino e avaliação |
| Pré-treino contínuo | Sim | Adaptar distribuição a corpus de domínio | Dados, compute e suporte pelo modelo |
| Pré-treino do zero | Sim | Modelo próprio com alto controle | Alto investimento e especialização |
| Distillation | Treina aluno | Modelo menor com comportamento útil do professor | Criar dados, treinar e medir perdas |

Podem ser combinados: modelo ajustado com RAG. Fine-tuning não é substituto padrão para consultar regulamento que muda diariamente. Agente acrescenta ferramentas e ações: RAG explica política; ferramenta autorizada consulta transação e pode iniciar processo sob controles.

#### 3.2 Engenharia de prompts

Estrutura: instrução clara + contexto relevante + entrada delimitada + restrições + formato esperado + exemplos quando úteis. Negative prompt diz o que evitar em modelos/modalidades compatíveis; não é barreira de segurança suficiente.

Zero-shot não fornece exemplo; single/one-shot fornece um; few-shot fornece alguns. Nenhuma dessas técnicas muda pesos. Chain-of-thought é técnica de decomposição/raciocínio exemplificado; não trate a exposição de raciocínio interno como prova de correção. Prefira etapas verificáveis e justificativa resumida adequada ao usuário.

Experimente, seja específico/conciso, decomponha tarefas e use múltiplas instruções/comentários de forma coerente. Versione prompts, parâmetros, exemplos e testes; Bedrock Prompt Management apoia gestão e reutilização. Compare qualidade/risco/custo com dataset estável.

Riscos: exposure revela instruções/dados; poisoning contamina treino/fontes; hijacking desvia tarefa; jailbreak contorna restrições; prompt injection introduz instruções maliciosas diretas ou por documento externo. Separar instrução de conteúdo, validar saída e limitar ferramentas reduz risco; um texto “ignore ataques” não garante proteção.

Template didático: “Use apenas os trechos autorizados fornecidos; responda em português com resumo e fontes; se não houver evidência, informe que não encontrou. Dados: [trechos]. Pergunta: [pergunta].” Ele organiza o comportamento, mas não implementa autorização.

#### 3.3 Treinamento e fine-tuning

Pré-treino aprende padrões gerais; pré-treino contínuo prossegue em corpus; instruction tuning usa exemplos de instrução/resposta; transfer learning reutiliza aprendizado; adaptação de domínio especializa; distillation usa professor para aluno. RLHF usa feedback/preferências humanas em alinhamento; revisão humana comum não é automaticamente RLHF.

Dados precisam de direitos de uso, origem, curadoria, limpeza, rótulos consistentes, representatividade e separação treino/teste. Quantidade adequada depende da tarefa/modelo; não existe número mágico. Evite duplicatas e PII desnecessária. Dados maiores e ruins podem piorar o modelo. Treinar para domínio pode degradar outros comportamentos, exigindo reavaliação.

#### 3.4 Avaliação de FM e aplicação

Avaliação automática usa datasets e métricas; human-in-the-loop avalia nuance, utilidade e riscos. Bedrock Model Evaluation fornece recursos conforme modelos/modalidades. Use baseline, critérios, conjunto separado e avaliação contínua.

- ROUGE mede sobreposição com referências, comum em resumo.
- BLEU compara n-gramas com penalização de brevidade, tradicional em tradução.
- BERTScore usa representações contextuais para similaridade semântica.
- LLM-as-a-judge usa modelo com rubrica; pode ter vieses, inclusive de posição/estilo, e precisa de calibração humana.
- RAG: relevância/recall da recuperação, correção, groundedness, cobertura e suporte das citações.
- Agentes: conclusão da tarefa, ferramenta correta, argumentos corretos, permissões, loops e número de passos.
- Workflows: resultado ponta a ponta e falhas por etapa.
- Negócio: conclusão de tarefas, satisfação, produtividade, engajamento, custo por interação e latência aceitável. Ajustar/decompor tarefas e seus critérios ajuda avaliar se o sistema resolve o problema real.

Métrica alta de similaridade não garante factualidade ou segurança. Se a fonte correta não foi recuperada, só ajustar o texto do prompt pode não resolver.

### Domínio 4 — IA responsável [D4]

#### 4.1 Desenvolvimento responsável

Bias é tendência sistemática que pode afetar grupos; fairness avalia equidade; inclusão contempla públicos/contextos diversos; robustez resiste a variações; safety evita danos; veracidade busca fatos corretos. Considere consumo e sustentabilidade na escolha do modelo. Guardrails é camada útil para conteúdo/tópicos/PII e verificações disponíveis, não garantia de risco zero.

Riscos incluem propriedade intelectual/licenças, discriminação, alucinações, dano ao usuário e perda de confiança. Curar fontes, diversificar dados, melhorar rótulos e analisar subgrupos ajuda mitigar. Dataset balanceado não elimina todos os vieses: proxies, rótulos, seleção e decisões do processo também importam.

Underfitting simplifica demais e erra treino/teste; overfitting aprende particularidades e vai bem no treino mas mal fora dele. Viés estatístico e viés discriminatório são conceitos diferentes. Audite humanos, rótulos e resultados, não apenas uma média global.

#### 4.2 Transparência e explicabilidade

Transparência informa propósito, dados, limitações, avaliação e condições de uso. Explicabilidade torna decisões compreensíveis. Modelo interpretável tem mecanismo mais acessível; explicação pós-hoc aproxima comportamento e tem limites. SageMaker Model Cards documenta; Bedrock Model Evaluations avalia; fontes abertas podem permitir inspeção, mas não garantem licença livre, dados conhecidos, equidade ou explicação perfeita.

Considere trade-offs entre segurança e divulgação, propriedade intelectual, interpretabilidade e performance. Design centrado no humano pede linguagem adequada, feedback, contestação e indicação de limites. Justificativa textual gerada pelo LLM não é evidência causal de como o sistema decidiu.

### Domínio 5 — Segurança, conformidade e governança [D5]

#### 5.1 Segurança de sistemas de IA

- Responsabilidade compartilhada: AWS protege infraestrutura; cliente controla dados, configuração, identidades e uso conforme serviço. Em EC2 há SO convidado sob responsabilidade do cliente; serviço gerenciado reduz, mas não elimina obrigações.
- IAM: roles, políticas e permissões de menor privilégio. Dê a cada ferramenta só acesso necessário; não transformar acesso ao chatbot em acesso administrador.
- Criptografia em repouso e trânsito; KMS gerencia chaves; Secrets Manager guarda/rotaciona credenciais; TLS protege trânsito.
- Macie identifica dados sensíveis no S3. PrivateLink pode fornecer conectividade privada onde suportado, sem conceder permissão automaticamente.
- AgentCore Identity e Policy apoiam identidade/controle de ações. Guardrails avalia conteúdo; são camadas distintas.
- Linhagem documenta origem/transformações/versões; catálogo organiza metadados; Model Cards registra modelo; citação liga resposta à fonte, mas ainda exige validar suporte e autorização.
- Engenharia segura: qualidade, integridade, privacidade, minimização, controle de acesso e tecnologias de proteção adequadas. Embedding não anonimiza automaticamente.
- Ameaças: injeção, vazamento, vulnerabilidade de software, toxicidade, uso indevido de ferramenta e saída malformada. Valide texto/JSON/código/SQL antes de executar ações.
- Registre trilha de auditoria e interações necessárias com minimização, retenção, criptografia e acesso restrito. CloudTrail não significa captura automática de todo prompt/resposta; isso depende de logging de invocação e observabilidade específicos.
- Grounding combina RAG, checagem contra fontes/sistemas e validação humana/automática. Confidence score precisa ser definido/calibrado; “tenho certeza” escrito pelo modelo não é probabilidade confiável.

#### 5.2 Governança e compliance

Config avalia configurações; Inspector avalia vulnerabilidades de workloads; Artifact fornece relatórios/acordos AWS; CloudTrail audita ações; Trusted Advisor recomenda boas práticas. Nenhum sozinho certifica o produto de IA.

Defina responsáveis, inventário, políticas, riscos, critérios de aprovação, versões e cadência/estratégia de revisão. Governança de dados cobre ciclo de vida, logging, residência, monitoramento, observação, retenção e exclusão. A exclusão pode precisar tratar origem, índice, memória, cache e cópias conforme política.

Generative AI Security Scoping Matrix ajuda entender responsabilidades conforme o grau de controle, de consumir aplicação até desenvolver/treinar modelos. Não é lei nem certificado. Estabeleça transparência e treinamento de equipe. Para produção, obrigações locais/setoriais devem ser confirmadas com jurídico/compliance; o exame não exige implementar um framework jurídico.

## 3. Métricas com exemplo de antifraude

| Métrica | Fórmula | Pergunta |
|---|---|---|
| Accuracy | (TP + TN) / total | Quantas previsões estavam corretas? |
| Precision | TP / (TP + FP) | Entre alertas, quantos eram fraude? |
| Recall | TP / (TP + FN) | Entre fraudes reais, quantas detectou? |
| F1 | 2 × precision × recall / (precision + recall) | Como combinar precision e recall? |

TP = fraude alertada; FP = compra legítima alertada; FN = fraude não detectada; TN = compra legítima liberada. Exemplo fictício: 1.000 transações, 20 fraudes, 30 alertas, 15 fraudes detectadas. TP=15, FP=15, FN=5, TN=965. Accuracy=98%, precision=50%, recall=75%, F1=60%. Sempre dizer “legítima” também produz 98% de accuracy e recall zero. Logo, accuracy isolada pode esconder fracasso na classe rara. Fórmulas têm convenções quando denominadores são zero.

Reduzir o limiar do mesmo score geralmente aumenta alertas/recall e pode reduzir precision; o compromisso depende de perdas de fraude, custo de revisão e atrito no cliente. F1 não incorpora automaticamente valores financeiros, calibração nem justiça.

## 4. Catálogo oficial — 51 entradas em 11 categorias [CAT]

Cada ficha contém o que é, uso, situação em que outra opção faz mais sentido, cobrança e distinções de prova. Não há alegação de frequência por serviço. Os links de produto/preço ficam ao final, por categoria.


### Analytics


#### AWS Data Exchange

- O que é: Catálogo e entrega de dados de fornecedores.
- Quando usar: Enriquecer datasets com fontes externas licenciadas.
- Quando não usar / alternativa: Para limpar dados próprios: Glue/DataBrew.
- Modelo de cobrança: Assinatura/contrato do fornecedor e modalidades de uso, com infraestrutura associada separada.
- Funcionalidades e pegadinhas de prova: Proveniência e licença importam; comprar dados não autoriza qualquer finalidade.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon EMR

- O que é: Plataforma para Spark/Hadoop e processamento distribuído.
- Quando usar: Preparar datasets massivos com PySpark.
- Quando não usar / alternativa: Para uma consulta pontual simples ou API pronta de IA.
- Modelo de cobrança: Taxa EMR mais infraestrutura no cluster; vCPU/memória/storage no Serverless.
- Funcionalidades e pegadinhas de prova: Processa dados, não é FM; cluster divide trabalho entre máquinas.
- Fonte: página oficial deste serviço na seção final [P].


#### AWS Glue

- O que é: Integração ETL serverless e catálogo.
- Quando usar: Catalogar e transformar dados para pipelines.
- Quando não usar / alternativa: Para treinar modelo: SageMaker AI.
- Modelo de cobrança: DPU-tempo, catálogo e recursos por uso.
- Funcionalidades e pegadinhas de prova: Crawler descobre esquema; Data Catalog guarda metadados, não o dataset.
- Fonte: página oficial deste serviço na seção final [P].


#### AWS Glue DataBrew

- O que é: Preparação visual por receitas.
- Quando usar: Limpar, perfilar e padronizar dados sem transformação manual em código.
- Quando não usar / alternativa: Para rotular imagens: Ground Truth.
- Modelo de cobrança: Sessões interativas e jobs/capacidade por tempo.
- Funcionalidades e pegadinhas de prova: Receita transforma dados; não é labeling nem treinamento.
- Fonte: página oficial deste serviço na seção final [P].


#### AWS Lake Formation

- O que é: Governança de acesso a data lakes.
- Quando usar: Controlar acesso granular a tabelas/colunas em recursos suportados.
- Quando não usar / alternativa: Para ETL: Glue; para chave criptográfica: KMS.
- Modelo de cobrança: Funções padrão sem taxa adicional; storage/compute e recursos integrados podem custar.
- Funcionalidades e pegadinhas de prova: Governança de acesso não valida exatidão dos dados.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon OpenSearch Service

- O que é: Busca textual e vetorial conforme configuração.
- Quando usar: Índice para recuperação semântica/RAG e busca híbrida.
- Quando não usar / alternativa: Para OLTP relacional: RDS.
- Modelo de cobrança: Instância+storage ou OCUs+storage Serverless; extras por recurso.
- Funcionalidades e pegadinhas de prova: Um modelo cria embeddings; índice os busca; não gera a resposta sozinho.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Quick

- O que é: Plataforma de analytics/produtividade e IA conforme componente.
- Quando usar: Dashboards e análise/acesso a conhecimento nos componentes contratados.
- Quando não usar / alternativa: Para treino customizado controlado: SageMaker AI.
- Modelo de cobrança: Assinatura, capacidade ou consumo por componente; conferir oferta.
- Funcionalidades e pegadinhas de prova: Não é apenas banco de dados; QuickSight é nome encontrado em materiais de BI anteriores.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Redshift

- O que é: Data warehouse analítico SQL.
- Quando usar: Analisar históricos e resultados de negócio em escala.
- Quando não usar / alternativa: Para transações curtas de cadastro: RDS.
- Modelo de cobrança: Nós provisionados ou RPU-tempo Serverless, storage e extras.
- Funcionalidades e pegadinhas de prova: OLAP agrega grandes históricos; OLTP serve transações operacionais.
- Fonte: página oficial deste serviço na seção final [P].


### Cloud Financial Management


#### AWS Budgets

- O que é: Orçamentos e alertas de custos/uso.
- Quando usar: Avisar gasto previsto/realizado de IA.
- Quando não usar / alternativa: Para estimativa antes de implantar: Calculator.
- Modelo de cobrança: Monitoramento padrão sem taxa; ações/relatórios seguem regras próprias.
- Funcionalidades e pegadinhas de prova: Alerta não é bloqueio rígido; ações precisam de configuração.
- Fonte: página oficial deste serviço na seção final [P].


#### AWS Cost Explorer

- O que é: Análise visual e por API de gastos.
- Quando usar: Investigar histórico e tendências.
- Quando não usar / alternativa: Para impor autorização/limite de ação: IAM e controles da aplicação.
- Modelo de cobrança: Interface padrão sem taxa; APIs/granularidades opcionais podem cobrar.
- Funcionalidades e pegadinhas de prova: Explorer analisa; Budgets alerta; Calculator estima.
- Fonte: página oficial deste serviço na seção final [P].


### Compute


#### Amazon EC2

- O que é: Máquina virtual configurável.
- Quando usar: Hospedar modelos/frameworks próprios, com GPU em tipos adequados.
- Quando não usar / alternativa: Se API gerenciada atende sem operação de servidor.
- Modelo de cobrança: Instância por tempo, On-Demand/Spot e descontos elegíveis; disco/rede à parte.
- Funcionalidades e pegadinhas de prova: Cliente administra SO convidado; Spot pode ser interrompida.
- Fonte: página oficial deste serviço na seção final [P].


#### AWS Lambda

- O que é: Funções acionadas por eventos sem gerir hosts.
- Quando usar: Validar entrada, integrar API e executar ferramenta curta.
- Quando não usar / alternativa: Para job acima de 15 minutos ou GPU/controle de host.
- Modelo de cobrança: Invocações, GB-segundo e extras; serviços chamados separados.
- Funcionalidades e pegadinhas de prova: Pode chamar um modelo, mas não é o modelo; limite de função não é duração máxima de todo agente.
- Fonte: página oficial deste serviço na seção final [P].


### Containers


#### Amazon Elastic Container Service (Amazon ECS)

- O que é: Orquestração nativa AWS de contêineres.
- Quando usar: Hospedar API/worker de inferência sem exigir Kubernetes.
- Quando não usar / alternativa: Se Kubernetes é requisito: EKS.
- Modelo de cobrança: Capacidade EC2/Fargate e infraestrutura; modos opcionais podem adicionar taxa.
- Funcionalidades e pegadinhas de prova: Task definition descreve execução; service mantém réplicas; não é registro de imagens.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Elastic Kubernetes Service (Amazon EKS)

- O que é: Kubernetes com plano de controle gerenciado.
- Quando usar: Workload de IA com requisito de API/ecossistema Kubernetes.
- Quando não usar / alternativa: Se ECS ou serviço de modelos resolve com menor complexidade.
- Modelo de cobrança: Cluster/tempo e suporte de versão, capacidade e extras.
- Funcionalidades e pegadinhas de prova: Pods rodam em nós; plano de controle gerenciado não opera automaticamente seu modelo.
- Fonte: página oficial deste serviço na seção final [P].


### Database


#### Amazon Aurora

- O que é: Banco relacional AWS compatível com MySQL/PostgreSQL.
- Quando usar: Transações e vetores no Aurora PostgreSQL com suporte adequado.
- Quando não usar / alternativa: Não presumir extensões PostgreSQL em toda engine Aurora.
- Modelo de cobrança: Instâncias ou ACUs, storage, I/O e backup conforme modalidade.
- Funcionalidades e pegadinhas de prova: Aurora pertence à família RDS; compatibilidade e versão determinam recurso vetorial.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon DocumentDB (with MongoDB compatibility)

- O que é: Banco de documentos com APIs MongoDB suportadas.
- Quando usar: Dados JSON e busca vetorial nas configurações compatíveis.
- Quando não usar / alternativa: Para compatibilidade integral presumida com MongoDB ou joins relacionais complexos.
- Modelo de cobrança: Instâncias/capacidade, storage, I/O e backups conforme oferta.
- Funcionalidades e pegadinhas de prova: Compatível não significa idêntico ao MongoDB; conferir matriz de recursos.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon DynamoDB

- O que é: NoSQL de chave-valor/documentos.
- Quando usar: Sessões, metadados e histórico com acesso por chave.
- Quando não usar / alternativa: Para joins ad hoc ou presumir busca semântica do histórico.
- Modelo de cobrança: Requisições on-demand ou capacidade provisionada, storage e extras.
- Funcionalidades e pegadinhas de prova: Guardar conversa não implementa automaticamente memória semântica.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon ElastiCache

- O que é: Dados em memória/cache gerenciado.
- Quando usar: Reduzir latência com cache de resultados/sessões.
- Quando não usar / alternativa: Como substituto automático do banco de referência durável.
- Modelo de cobrança: Nós por tempo ou Serverless por storage/capacidade conforme engine.
- Funcionalidades e pegadinhas de prova: Cache deve respeitar identidade/tenant; não compartilhar resposta privada indevidamente.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Neptune

- O que é: Família de bancos e analytics de grafos.
- Quando usar: Vínculos entre entidades e GraphRAG; vetores conforme produto/configuração.
- Quando não usar / alternativa: Para CRUD simples por chave ou supor recursos iguais em toda edição.
- Modelo de cobrança: Instâncias/capacidade, storage/I/O ou capacidade analítica conforme produto.
- Funcionalidades e pegadinhas de prova: Nós/arestas representam relações; recursos de Neptune Analytics não são universais em Neptune Database.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon RDS

- O que é: Bancos relacionais gerenciados de diversas engines.
- Quando usar: SQL transacional; PostgreSQL com pgvector quando compatível.
- Quando não usar / alternativa: Para controle total do SO ou engine não suportada.
- Modelo de cobrança: Instância, storage, I/O, backup e descontos elegíveis.
- Funcionalidades e pegadinhas de prova: Vetor em PostgreSQL não significa o mesmo suporte em toda engine RDS.
- Fonte: página oficial deste serviço na seção final [P].


### Developer Tools


#### Kiro

- O que é: Ferramentas de desenvolvimento assistido por IA e agentes.
- Quando usar: Apoiar especificação, código, testes e tarefas de desenvolvimento.
- Quando não usar / alternativa: Como API genérica de inferência para usuários finais ou substituto de revisão.
- Modelo de cobrança: Planos com créditos e assinaturas, extras conforme contrato.
- Funcionalidades e pegadinhas de prova: Código gerado pode estar errado/vulnerável; testar e proteger contexto.
- Fonte: página oficial deste serviço na seção final [P].


#### Strands Agents

- O que é: SDK open source para agentes orientados por modelos.
- Quando usar: Programar agente, ferramentas e integrações como MCP.
- Quando não usar / alternativa: Se uma chamada simples ou workflow determinístico é suficiente.
- Modelo de cobrança: SDK sem taxa de licença de serviço; modelo, runtime e ferramentas cobrados à parte.
- Funcionalidades e pegadinhas de prova: SDK não hospeda automaticamente o agente; AgentCore pode fornecer runtime.
- Fonte: página oficial deste serviço na seção final [P].


### Machine Learning


#### Amazon Bedrock

- O que é: Plataforma gerenciada de FMs e aplicações generativas.
- Quando usar: Consumir modelos, RAG, guardrails, avaliação e agentes.
- Quando não usar / alternativa: Se precisa de controle de treino/ambiente além do suportado: SageMaker AI/compute.
- Modelo de cobrança: Tokens/mídia, capacidade, customização e recursos por uso.
- Funcionalidades e pegadinhas de prova: Bedrock é plataforma, Nova é família de modelos; ver seção de recursos.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Bedrock AgentCore

- O que é: Componentes gerenciados para operação de agentes.
- Quando usar: Runtime, gateway, identidade, memória, políticas e observabilidade.
- Quando não usar / alternativa: Se só precisa chamar um FM sem ferramentas/estado.
- Modelo de cobrança: Consumo por componente; inferência/ferramentas e infraestrutura conforme modalidade separadas.
- Funcionalidades e pegadinhas de prova: Strands é SDK; AgentCore opera componentes; Identity/Policy não são filtro de conteúdo.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Comprehend

- O que é: NLP para interpretação de texto.
- Quando usar: Entidades, sentimento, frases-chave e classificação customizada.
- Quando não usar / alternativa: Para áudio bruto: Transcribe; para OCR: Textract.
- Modelo de cobrança: Unidades de texto e treino/inferência customizados conforme API.
- Funcionalidades e pegadinhas de prova: Compreender texto difere de transcrever fala e ler imagem.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Lex

- O que é: Interfaces conversacionais de voz/texto.
- Quando usar: Bot de intenções e coleta de parâmetros.
- Quando não usar / alternativa: Para síntese de fala isolada: Polly; para conversa aberta avaliar FM.
- Modelo de cobrança: Solicitações de texto/voz e modalidade conversacional.
- Funcionalidades e pegadinhas de prova: Intent é objetivo; slot é parâmetro; fulfillment executa atendimento.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Nova

- O que é: Família de modelos Amazon.
- Quando usar: Compreensão e geração nas modalidades específicas do modelo.
- Quando não usar / alternativa: Não assumir que todo modelo da família faz tudo.
- Modelo de cobrança: Tokens, mídia e unidades conforme modelo/acesso.
- Funcionalidades e pegadinhas de prova: Família não é plataforma; comparar capacidades em vez de decorar nome da versão.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Personalize

- O que é: Recomendação personalizada com ML.
- Quando usar: Ranking de produtos/conteúdo com dados de usuários e interações.
- Quando não usar / alternativa: Para responder sobre normas internas atuais.
- Modelo de cobrança: Ingestão, treino, campanhas/recommenders e inferência conforme modalidade.
- Funcionalidades e pegadinhas de prova: Recomendação não é apenas redigir sugestão; avaliar mínimos de capacidade e dados.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Polly

- O que é: Text-to-speech.
- Quando usar: Ler respostas e conteúdo em voz.
- Quando não usar / alternativa: Para transcrever: Transcribe.
- Modelo de cobrança: Caracteres e tipo de voz.
- Funcionalidades e pegadinhas de prova: Texto → voz; SSML controla elementos de fala quando suportado.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Rekognition

- O que é: Análise de imagens/vídeos.
- Quando usar: Objetos, cenas e moderação visual.
- Quando não usar / alternativa: Para formulários/tabelas: Textract; para gerar imagem: FM.
- Modelo de cobrança: Imagens, minutos de vídeo e extras por API.
- Funcionalidades e pegadinhas de prova: Reconhecer não é gerar; tratar scores e riscos de reconhecimento adequadamente.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon SageMaker AI

- O que é: Desenvolvimento, treino, adaptação e implantação de ML.
- Quando usar: Criar modelo próprio e gerenciar ciclo de vida.
- Quando não usar / alternativa: Se API pronta ou Bedrock atende com menor esforço.
- Modelo de cobrança: Compute, treino, endpoints, storage, processamento e recursos; descontos elegíveis.
- Funcionalidades e pegadinhas de prova: Treino e hospedagem têm custos diferentes; endpoint provisionado pode cobrar ocioso.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon SageMaker JumpStart

- O que é: Modelos e soluções iniciais no SageMaker AI.
- Quando usar: Experimentar e implantar pré-treinados com menos montagem.
- Quando não usar / alternativa: Se quer só API gerenciada de FM sem administrar endpoint.
- Modelo de cobrança: Sem taxa adicional do catálogo; recursos de treino/inferência/storage e eventuais termos/licenças.
- Funcionalidades e pegadinhas de prova: Pré-treinado não significa uso irrestrito nem implantação grátis.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Textract

- O que é: OCR e extração estruturada de documentos.
- Quando usar: Ler texto, formulários, tabelas e recursos documentais suportados.
- Quando não usar / alternativa: Para sentimento: Comprehend; para imagens genéricas: Rekognition.
- Modelo de cobrança: Páginas e tipo de API/recurso.
- Funcionalidades e pegadinhas de prova: Extrair campos não é raciocinar sobre toda a documentação; pode compor pipeline com RAG.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Transcribe

- O que é: Speech-to-text.
- Quando usar: Converter gravações/streaming em texto.
- Quando não usar / alternativa: Para gerar voz: Polly; para traduzir texto: Translate.
- Modelo de cobrança: Duração de áudio e recursos/modalidade.
- Funcionalidades e pegadinhas de prova: Voz → texto; diarização distingue falantes onde suportado.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Translate

- O que é: Tradução automática de texto.
- Quando usar: Traduzir mensagens/documentos entre idiomas suportados.
- Quando não usar / alternativa: Para áudio bruto sem transcrição ou para sentimento.
- Modelo de cobrança: Caracteres e modalidade/customização.
- Funcionalidades e pegadinhas de prova: Terminologia orienta vocabulário; tradução exige avaliação de domínio.
- Fonte: página oficial deste serviço na seção final [P].


#### AWS Transform

- O que é: Experiência agêntica para modernização de aplicações/código/infraestrutura.
- Quando usar: Analisar e transformar workloads suportados.
- Quando não usar / alternativa: Para agente corporativo genérico ou treinamento de FM.
- Modelo de cobrança: Casos/avaliações elegíveis sem taxa; custom/modernização contínua têm cobrança conforme oferta, como agente-minuto; recursos associados separados.
- Funcionalidades e pegadinhas de prova: Não é tudo gratuito nem substitui testes e aprovação de alterações.
- Fonte: página oficial deste serviço na seção final [P].


### Management and Governance


#### AWS CloudTrail

- O que é: Auditoria de eventos/chamadas AWS cobertos.
- Quando usar: Identificar quem fez alteração e quando.
- Quando não usar / alternativa: Para CPU/latência: CloudWatch; para pressupor todos os prompts registrados.
- Modelo de cobrança: Histórico padrão de gerenciamento por 90 dias sem taxa; eventos/cópias/Lake conforme uso.
- Funcionalidades e pegadinhas de prova: Data events e logging de conteúdo requerem verificar suporte/configuração.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon CloudWatch

- O que é: Métricas, logs, alarmes e observabilidade.
- Quando usar: Monitorar latência, erros e consumo da aplicação.
- Quando não usar / alternativa: Para provar factualidade/equidade sem avaliação específica.
- Modelo de cobrança: Métricas, ingestão/retenção/consulta de logs, alarmes e extras.
- Funcionalidades e pegadinhas de prova: Qualidade operacional não é qualidade semântica; logs podem conter PII.
- Fonte: página oficial deste serviço na seção final [P].


#### AWS Config

- O que é: Histórico de configurações e regras de conformidade.
- Quando usar: Detectar recursos fora de políticas.
- Quando não usar / alternativa: Para saber identidade de cada chamada: CloudTrail.
- Modelo de cobrança: Itens registrados e avaliações de regras/conformance packs.
- Funcionalidades e pegadinhas de prova: Detectar não é bloquear/corrigir automaticamente.
- Fonte: página oficial deste serviço na seção final [P].


#### AWS Trusted Advisor

- O que é: Recomendações de boas práticas.
- Quando usar: Revisar riscos de custo, segurança e outros pilares cobertos.
- Quando não usar / alternativa: Para certificar modelo ou analisar respostas em tempo real.
- Modelo de cobrança: Acesso a checks/APIs depende de plano de suporte.
- Funcionalidades e pegadinhas de prova: Recomenda, não aplica necessariamente; não é certificado regulatório.
- Fonte: página oficial deste serviço na seção final [P].


#### AWS Well-Architected Tool

- O que é: Revisão guiada de arquitetura.
- Quando usar: Registrar riscos e melhorias da solução.
- Quando não usar / alternativa: Para scan contínuo de CVEs: Inspector.
- Modelo de cobrança: Ferramenta sem taxa adicional; serviços utilizados são cobrados.
- Funcionalidades e pegadinhas de prova: Seis pilares: excelência operacional, segurança, confiabilidade, performance, custos e sustentabilidade.
- Fonte: página oficial deste serviço na seção final [P].


### Networking and Content Delivery


#### Amazon CloudFront

- O que é: CDN de entrega pela borda.
- Quando usar: Acelerar frontend e conteúdo reutilizável elegível.
- Quando não usar / alternativa: Para cache indiscriminado de respostas privadas ou para treinar FM.
- Modelo de cobrança: Transferência/requisições/extras ou planos fixos conforme oferta.
- Funcionalidades e pegadinhas de prova: CDN não é banco vetorial nem GPU global; respeitar autorização no cache.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon VPC

- O que é: Rede virtual isolada regional.
- Quando usar: Isolar componentes e fornecer caminhos privados quando suportados.
- Quando não usar / alternativa: Como substituto de IAM ou validação de conteúdo.
- Modelo de cobrança: VPC básica sem taxa; NAT, endpoints, IPv4 público e outros componentes podem cobrar.
- Funcionalidades e pegadinhas de prova: Subnet pertence a uma AZ; rede privada não dá permissão de dados automaticamente.
- Fonte: página oficial deste serviço na seção final [P].


### Security, Identity, and Compliance


#### AWS Artifact

- O que é: Portal de evidências/acordos de compliance AWS.
- Quando usar: Obter relatórios como SOC e certificações disponíveis.
- Quando não usar / alternativa: Para certificar automaticamente a aplicação de IA.
- Modelo de cobrança: Sem taxa direta.
- Funcionalidades e pegadinhas de prova: Conformidade da infraestrutura AWS não valida todo uso da aplicação.
- Fonte: página oficial deste serviço na seção final [P].


#### AWS Identity and Access Management (IAM)

- O que é: Autorização/autenticação de recursos AWS.
- Quando usar: Roles temporárias e menor privilégio em modelos/ferramentas.
- Quando não usar / alternativa: Para filtrar toxicidade ou guardar senha textual.
- Modelo de cobrança: Recursos básicos sem taxa; funções especializadas podem cobrar.
- Funcionalidades e pegadinhas de prova: Deny explícito prevalece; policy autoriza/limita, não é a identidade.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Inspector

- O que é: Gestão de vulnerabilidades em workloads suportados.
- Quando usar: Verificar EC2, imagens ECR e Lambda conforme cobertura.
- Quando não usar / alternativa: Para achar PII: Macie; para medir alucinação: avaliação.
- Modelo de cobrança: Recursos monitorados e escaneamentos conforme modalidade.
- Funcionalidades e pegadinhas de prova: CVE de pacote não é viés nem erro factual de resposta.
- Fonte: página oficial deste serviço na seção final [P].


#### AWS Key Management Service (AWS KMS)

- O que é: Gerenciamento de chaves criptográficas.
- Quando usar: Criptografia integrada e políticas de chave.
- Quando não usar / alternativa: Para armazenar API key textual: Secrets Manager.
- Modelo de cobrança: Chaves gerenciadas pelo cliente, chamadas e recursos conforme tipo.
- Funcionalidades e pegadinhas de prova: Criptografia não impede uso indevido de quem tem acesso legítimo.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon Macie

- O que é: Descoberta de dados sensíveis no S3.
- Quando usar: Identificar PII em datasets/documentos armazenados no S3.
- Quando não usar / alternativa: Para examinar automaticamente todos os bancos/prompts.
- Modelo de cobrança: Inventário/avaliação e descoberta conforme objetos/bytes e modalidade.
- Funcionalidades e pegadinhas de prova: Descobrir não significa remover ou autorizar uso automaticamente.
- Fonte: página oficial deste serviço na seção final [P].


#### AWS Secrets Manager

- O que é: Armazenamento/rotação de segredos.
- Quando usar: Entregar senha/API key à aplicação sem pôr no prompt.
- Quando não usar / alternativa: Para armazenar dataset ou gerir chave criptográfica KMS.
- Modelo de cobrança: Segredos armazenados e chamadas; rotação pode usar recursos pagos.
- Funcionalidades e pegadinhas de prova: Rotação precisa de suporte/configuração; modelo não precisa ler o valor do segredo.
- Fonte: página oficial deste serviço na seção final [P].


### Storage


#### Amazon S3

- O que é: Armazenamento de objetos em buckets.
- Quando usar: Datasets, documentos RAG, artefatos, logs e batch.
- Quando não usar / alternativa: Para disco de boot/OLTP relacional.
- Modelo de cobrança: GB-mês, operações, transferência, recuperação e extras por classe.
- Funcionalidades e pegadinhas de prova: Versionamento preserva versões, não aprova modelo; lifecycle transiciona/expira; controlar acesso.
- Fonte: página oficial deste serviço na seção final [P].


#### Amazon S3 Glacier

- O que é: Classes S3 de arquivo.
- Quando usar: Reter histórico com baixa frequência de acesso e prazo de recuperação compatível.
- Quando não usar / alternativa: Para fonte RAG continuamente consultada, sobretudo com restauração lenta.
- Modelo de cobrança: Storage, operações, recuperação e retenção mínima por classe.
- Funcionalidades e pegadinhas de prova: Instant Retrieval: milissegundos; Flexible: minutos/horas; Deep Archive: horas.
- Fonte: página oficial deste serviço na seção final [P].


## 5. Bedrock — funcionalidades detalhadas

Referências: [D2], [D3], [D4], [D5], [P-Bedrock]. O guia cita nominalmente Knowledge Bases, Guardrails, Prompt Management e Model Evaluation. Cache, customização, distillation, agentes e capacidade também ajudam a interpretar os objetivos; recursos individuais podem variar por modelo e Região.

| Recurso | O que faz / quando usar | Limite ou pegadinha | O que gera custo |
|---|---|---|---|
| Inferência por API | Executa FM para uma tarefa | Consultar não treina automaticamente o modelo | Tokens de entrada/saída ou mídia/modelo |
| Knowledge Bases | Ingestão e recuperação para RAG | Não altera pesos; acesso deve respeitar usuário | Embeddings, parsing/ingestão, backend, consultas e geração conforme configuração |
| Agents | Coordena ferramentas e fontes para tarefa | Não é só chatbot; ações precisam de escopo | Inferência de orquestração e serviços/ferramentas usados |
| Guardrails | Filtros de conteúdo, tópicos e dados sensíveis, verificações conforme recurso | Não equivale a IAM nem elimina todo erro | Unidades de conteúdo/verificações por recurso |
| Prompt Management | Testa, versiona e reutiliza templates/configurações | Template não é treinamento | Testes/inferência e recursos associados conforme oferta |
| Model Evaluation | Avaliação automática/humana ou por juiz conforme suporte | Benchmark isolado não valida produção | Inferência, avaliação e trabalho humano conforme modalidade |
| Prompt caching | Reutiliza prefixos/contexto elegíveis | Não é cache de resposta nem memória permanente | Escrita/leitura de cache e tokens conforme modelo |
| Fine-tuning/customização | Altera comportamento de modelos suportados | Não disponível da mesma forma para todos | Treino, storage e forma de servir o modelo |
| Distillation | Treina aluno com comportamento útil do professor | Há possível perda de qualidade; reavaliar | Geração de dados, treinamento e inferência |
| Provisioned Throughput | Capacidade comprada nos modelos elegíveis | Pode cobrar ociosa; não é sempre a melhor opção | Unidades/capacidade por tempo e compromisso |
| Batch inference | Processa conjunto de entradas sem interação imediata | Não serve para chat que requer resposta síncrona | Modalidade batch e serviços associados |

### Analogia: escritor, biblioteca, editor e crachá

O FM é um escritor que aprendeu padrões lendo. O prompt é a encomenda. RAG coloca livros selecionados sobre a mesa; Knowledge Bases organiza localização e entrega. Fine-tuning muda hábitos do escritor com formação adicional. Guardrails é uma camada de revisão; IAM é o crachá que controla acesso às salas e ferramentas. Um editor não substitui o crachá; o crachá não verifica se uma frase é verdadeira. Citação indica a fonte usada, não valida a conclusão automaticamente.

### Comparação de cenários

- Manual muda toda semana e precisa de fontes: avaliar RAG.
- Saída tem formato simples: começar com instrução, template e validação de esquema.
- Estilo/tarefa precisa de adaptação consistente em muitos exemplos: avaliar fine-tuning depois de baseline com prompt.
- Modelo grande é caro para tarefa estreita: avaliar modelo menor, roteamento ou distillation com testes.
- Precisa atualizar transação: ferramenta/API e autorização; documento RAG não executa operação.
- Não há evidência: abster-se/escalar pode ser melhor do que completar uma resposta inventada.

## 6. SageMaker AI — recursos para reconhecer

Referências: [D1], [D4], [P-SageMaker]. Além de Model Cards, citado pelo guia, os recursos abaixo ilustram etapas do ciclo de ML; não são todos objetivos nominais independentes.

| Funcionalidade | Papel e uso | Limite/pegadinha | Cobrança predominante |
|---|---|---|---|
| Studio | Ambiente integrado de desenvolvimento | Interface não é endpoint de produção | Compute/storage e serviços iniciados |
| Notebooks/JupyterLab | Explorar, preparar e desenvolver | Fechar navegador não garante parar compute | Instância por tempo e storage |
| Canvas | Interface visual/no-code | No-code não remove avaliação/governança | Sessões, construção/inferência e recursos conforme oferta |
| Autopilot | Automatiza etapas de AutoML | Precisa de dados adequados e objetivo certo | Processamento, treino e implantação |
| Ground Truth | Rotular dados com opções humanas/automação | Rotular não treina o classificador de negócio | Objetos/tarefas, trabalho humano e recursos |
| Data Wrangler | Preparar/explorar/transformar dados | Não é modelo treinado | Instâncias/jobs conforme ambiente |
| Feature Store | Reutilizar atributos de treino/inferência | Feature não é peso nem necessariamente embedding | Leituras/escritas, capacidade e storage |
| Training jobs | Treino gerenciado | Encerrar notebook não encerra todos os jobs | Instância/tempo; customização gerenciada pode usar tokens |
| Real-time endpoints | Inferência síncrona | Endpoint provisionado pode cobrar sem chamadas | Capacidade/instâncias e recursos associados |
| Serverless Inference | Inferência sem gerir servidores | Suporte/limites e cold starts importam | Duração/memória, dados e concorrência provisionada opcional |
| Asynchronous Inference | Enfileira solicitação e entrega depois | Não atende todo requisito de resposta instantânea | Instância/capacidade e storage |
| Batch Transform | Predições em datasets | Não é endpoint interativo | Instâncias pelo tempo do job |
| Experiments | Comparar e rastrear experimentos | Métrica técnica não decide sozinha objetivo de negócio | Execução/storage e componentes utilizados |
| Pipelines | Encadear etapas repetíveis | Cada etapa consome recursos | Jobs/serviços executados |
| Model Registry | Versões, metadados e aprovação | Registrar não significa aprovar/implantar automaticamente | Recursos associados conforme uso |
| Model Monitor | Monitorar dados/modelo e drift conforme configuração | Pode precisar de baseline e rótulos reais | Jobs de monitoramento, captura e storage |
| Clarify | Analisar viés e explicar comportamento | Não certifica justiça ou causalidade | Jobs/compute e recursos de explicação |
| Model Cards | Documentar propósito, treino, avaliação e limites | Documentação não corrige o modelo | Recursos associados; conferir modalidade |
| JumpStart | Modelos/soluções prontos para iniciar | Deploy pode criar endpoint cobrado | Treino/inferência/storage e termos do modelo |

### Analogia: serviço especializado versus oficina equipada

Bedrock se parece com contratação de capacidades por interface padronizada; SageMaker AI é uma oficina equipada para construir, adaptar e operar soluções com mais controle. JumpStart é a estante de kits da oficina. Não leve a analogia ao extremo: Bedrock também permite customização, e SageMaker AI também usa modelos pré-treinados. O requisito define o equilíbrio entre controle, responsabilidade e operação.

## 7. IA agêntica: conectando as peças

Referências: [D2], [D5] e links de Strands, AgentCore, Kiro e Transform.

Strands Agents é SDK: código/framework para construir o comportamento do agente. AgentCore oferece componentes gerenciados de execução e operação que podem atender diferentes frameworks. MCP é protocolo de integração com ferramentas/contexto. Kiro auxilia desenvolvimento. Transform é orientado à modernização. Não são cinco nomes para um mesmo chatbot.

| Componente | Função | Não confundir com |
|---|---|---|
| Modelo | Interpreta contexto e propõe saída/ação | Sistema de autorização |
| Runtime | Executa o código do agente | Modelo de linguagem |
| Gateway | Facilita conexão/exposição de ferramentas | Banco de memória |
| Identity | Integra identidades e acesso a credenciais | Filtro de toxicidade |
| Policy | Restringe ações conforme regras suportadas | Prompt “seja cuidadoso” |
| Memory | Retém contexto/informação conforme política | Janela ilimitada ou anonimização |
| Observabilidade | Ajuda rastrear execução e falhas | Garantia de comportamento correto |
| Guardrails | Verifica/aplica políticas de conteúdo | Permissão para alterar conta bancária |

Analogia: agente é um analista; FM auxilia decisões; ferramentas são os sistemas; Strands é o kit que organiza o trabalho; runtime é o escritório; identidade é o crachá; política diz o que pode fazer; MCP é padrão de conexão; memória é o caderno. Um documento recebido pelo analista não pode virar ordem administrativa só porque contém frases imperativas.

Uma tarefa pode gerar dez chamadas de modelo, várias ferramentas e armazenamento de memória. Limite iterações, tempo, gasto, concorrência e escopo; defina condição de parada e escalonamento. Exija validação/aprovação para atos sensíveis. Multiagentes pode ajudar especialização, mas workflow determinístico costuma ser mais previsível quando o fluxo já é conhecido.

## 8. Infraestrutura e dados — analogias didáticas

### VM, contêiner, ECS, Kubernetes e EKS

VM é apartamento com cozinha própria: há SO convidado. Imagem de contêiner é pacote/receita com aplicação/dependências; contêiner é execução que compartilha o kernel do host. ECS é gerente de execuções nativo AWS. Kubernetes é orquestrador com API/ecossistema próprios: agrupa contêineres em pods, agenda em nós e mantém estado desejado. EKS fornece plano de controle Kubernetes gerenciado. Nenhum é modelo de IA por si só: podem executar sua API de inferência.

Complemento para entender a infraestrutura, sem tratá-los como entradas extras do catálogo: ECR armazena imagens; Fargate oferece capacidade sem administrar hosts em configurações ECS/EKS suportadas. O pacote, o gerente e a capacidade são papéis distintos.

### VPC e camadas de rede

VPC é condomínio de rede; subnet é área dentro de uma AZ; tabela de rotas define saídas. Security group é portaria stateful que permite tráfego e reconhece retorno; NACL é cancela stateless de subnet com permitir/negar e análise separada de ida/volta. Porta TCP pertence ao transporte; requisição HTTP pertence à aplicação. Abrir porta não valida conteúdo do prompt.

PrivateLink fornece caminho privado para serviço suportado; IAM define acesso; KMS protege dados em repouso; TLS protege trânsito; Guardrails trata conteúdo. Não substitua uma camada por outra. NAT e endpoints podem gerar custo mesmo quando a VPC básica não tem tarifa própria.

### Lake, catálogo, warehouse, índice e grafo

S3 é depósito de objetos; Glue Data Catalog é fichário dos metadados; Lake Formation administra acesso; Glue/EMR preparam dados; Redshift é estrutura para grandes análises SQL; OpenSearch é índice de busca; Neptune representa vínculos. Embedding é endereço semântico num espaço numérico, não documento cifrado.

Num cenário de antifraude: RDS registra operações; DynamoDB pode guardar estado por chave; Neptune explora vínculos entre contas/dispositivos; Redshift agrega tendências; ElastiCache acelera acesso repetido. Um modelo classifica risco; um LLM pode explicar evidência autorizada sem virar, por isso, um classificador validado.

## 9. Custos: raciocínio em vez de decorar preços

Referências: [P-Bedrock], [P-SageMaker] e páginas de cada serviço.

Para texto, um raciocínio simplificado é: custo de entrada = tokens de entrada ÷ unidade de preço × preço da entrada; custo de saída usa fórmula análoga. Some os dois e componentes auxiliares. A tabela pode usar 1.000 ou 1 milhão de tokens. Mensagens de sistema, histórico reenviado, documentos e esquemas de ferramentas podem compor entrada. Saída pode ter preço diferente; imagens/áudio/vídeo podem usar outras métricas.

RAG adiciona ingestão, parsing, embeddings, armazenamento, consultas vetoriais, possível reranking e inferência. Fine-tuning adiciona dados, treino, armazenamento e forma de servir; alguns métodos cobram tokens processados por época, outros compute/tempo. Agentes multiplicam chamadas conforme passos e ferramentas. Não existe preço universal por “uma pergunta”.

| Decisão | Benefício possível | Trade-off |
|---|---|---|
| Modelo menor adequado | Menor custo/latência | Pode perder capacidade |
| Contexto enxuto e relevante | Menos tokens e ruído | Pode omitir evidência necessária |
| Cache elegível | Reuso mais barato/rápido | Validade, isolamento e suporte variam |
| Batch | Boa economia para trabalho sem urgência | Não entrega interação imediata |
| Endpoint/capacidade provisionada | Latência/capacidade previsíveis | Pode cobrar ocioso |
| Serverless | Ajusta capacidade ao uso | Limites/cold start e preço por carga |
| Mais redundância/regiões | Resiliência/cobertura | Maior custo e governança de dados |
| Limitar loops e retries | Controla gasto e falhas repetidas | Precisa de condição de escalonamento |

Meça custo por tarefa resolvida com qualidade, não apenas por chamada. Parar notebook não garante desligar endpoint. Budgets alerta, Explorer investiga gasto, Calculator estima. Nenhum é substituto de limites da aplicação.

## 10. Pegadinhas consolidadas

| Confusão | Distinção correta |
|---|---|
| Palavra = token | Tokenização varia por idioma/modelo |
| Temperatura baixa = verdade | Reduzir aleatoriedade não valida fatos |
| Janela de contexto = memória permanente | Contexto processado e persistência são diferentes |
| Few-shot muda pesos | Só fornece exemplos no contexto |
| Fine-tuning atualiza automaticamente fatos diários | RAG/consulta externa costuma ser mais apropriado |
| RAG elimina alucinação | Recuperação/geração ainda precisam de avaliação |
| Citação garante resposta correta | Verificar se fonte realmente sustenta a afirmação |
| Embedding anonimiza | Vetores podem continuar sensíveis |
| Nova = Bedrock | Família de modelos versus plataforma |
| Strands = AgentCore | SDK versus componentes operacionais |
| MCP concede acesso | Integração não é autorização |
| Guardrails substitui IAM | Conteúdo e autorização são camadas diferentes |
| PrivateLink permite qualquer documento | Caminho privado não concede permissão |
| Macie examina tudo | Descoberta de dados sensíveis tem foco no S3 |
| Inspector detecta alucinação | Trata vulnerabilidades de workloads suportados |
| CloudWatch prova fairness | Observabilidade precisa de métricas/testes próprios |
| CloudTrail grava todo prompt por padrão | Cobertura de eventos/logging de conteúdo é distinta |
| Model Card corrige viés | Documenta; intervenção exige processo |
| Artifact certifica minha IA | Fornece evidências AWS, não certificação universal da aplicação |
| Accuracy basta na classe rara | Precision/recall e custo dos erros importam |
| Dataset balanceado elimina viés | Origem, rótulos e proxies também importam |
| Open source autoriza tudo | Conferir licença de código/pesos/dados |
| LLM-as-a-judge dispensa humanos | Calibrar juiz e avaliar seus vieses |
| ROUGE alto comprova factualidade | Sobreposição textual não verifica verdade |
| Serverless sempre é mais barato | Depende de carga, modalidade e latência |
| Todo Glacier demora horas | Instant Retrieval tem acesso em milissegundos |
| Toda engine RDS tem o mesmo vetor | Engine/extensão/versão determinam suporte |
| Todo caso precisa de agente | Regras e workflows podem ser melhores |

## 11. Checklist de revisão

- Explico IA/ML/deep learning/GenAI/agentes sem confundir categorias?
- Escolho classificação/regressão/clustering/previsão/recomendação ou regra determinística?
- Sei treino, inferência, batch, assíncrona, tempo real e serverless?
- Interpreto precisão, recall, F1 e accuracy em dados desbalanceados?
- Diferencio prompt, contexto, memória, RAG e fine-tuning?
- Consigo explicar tokens, embeddings, chunking, transformer e difusão?
- Seleciono FM por tarefa, qualidade medida, risco, modalidade, latência e custo?
- Diferencio métricas de modelo, aplicação e negócio?
- Explico SDK, runtime, ferramenta, identidade, política e MCP?
- Distingo explicabilidade, transparência, fairness, robustez e segurança?
- Conheço função, melhor uso e unidade de custo das 51 entradas?
- Sei que cobertura publicada não significa lista fechada da prova?

## 12. Links oficiais para o NotebookLM

Todos os URLs estão nesta seção. Os marcadores ao longo do texto remetem a estas fontes. Escopo vem do guia; detalhes operacionais/preços devem ser confirmados nas páginas vigentes. Links complementares de recursos ajudam estudar, sem ampliar artificialmente a lista oficial.


### Guias e funcionalidades

- [G] Guia oficial AIF-C01: https://docs.aws.amazon.com/aws-certification/latest/ai-practitioner-01/ai-practitioner-01.html
- [CAT] Serviços em escopo: https://docs.aws.amazon.com/aws-certification/latest/ai-practitioner-01/aif-01-in-scope-services.html
- [D1] Domínio 1: https://docs.aws.amazon.com/aws-certification/latest/ai-practitioner-01/ai-practitioner-01-domain1.html
- [D2] Domínio 2: https://docs.aws.amazon.com/aws-certification/latest/ai-practitioner-01/ai-practitioner-01-domain2.html
- [D3] Domínio 3: https://docs.aws.amazon.com/aws-certification/latest/ai-practitioner-01/ai-practitioner-01-domain3.html
- [D4] Domínio 4: https://docs.aws.amazon.com/aws-certification/latest/ai-practitioner-01/ai-practitioner-01-domain4.html
- [D5] Domínio 5: https://docs.aws.amazon.com/aws-certification/latest/ai-practitioner-01/ai-practitioner-01-domain5.html
- Serviços fora do escopo: https://docs.aws.amazon.com/aws-certification/latest/ai-practitioner-01/aif-01-out-of-scope-services.html
- Guia em português (PDF): https://docs.aws.amazon.com/pt_br/aws-certification/latest/ai-practitioner-01/ai-practitioner-01.pdf
- [P-Bedrock] Preços Bedrock: https://aws.amazon.com/bedrock/pricing/
- [P-SageMaker] Preços SageMaker AI: https://aws.amazon.com/sagemaker/ai/pricing/
- Preços AWS: https://aws.amazon.com/pricing/
- AWS Pricing Calculator: https://calculator.aws/
- Visão geral AI/ML AWS: https://docs.aws.amazon.com/whitepapers/latest/aws-overview/machine-learning.html
- Responsabilidade compartilhada: https://aws.amazon.com/compliance/shared-responsibility-model/
- Documentação Bedrock: https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html
- Knowledge Bases: https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html
- Guardrails: https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails.html
- Agents: https://docs.aws.amazon.com/bedrock/latest/userguide/agents.html
- Prompt Management: https://docs.aws.amazon.com/bedrock/latest/userguide/prompt-management.html
- Model Evaluation: https://docs.aws.amazon.com/bedrock/latest/userguide/evaluation.html
- Proteção de dados Bedrock: https://docs.aws.amazon.com/bedrock/latest/userguide/data-protection.html
- Documentação SageMaker AI: https://docs.aws.amazon.com/sagemaker/latest/dg/whatis.html
- Model Cards: https://docs.aws.amazon.com/sagemaker/latest/dg/model-cards.html
- Clarify: https://docs.aws.amazon.com/sagemaker/latest/dg/clarify-fairness-and-explainability.html
- Model Monitor: https://docs.aws.amazon.com/sagemaker/latest/dg/model-monitor.html
- Feature Store: https://docs.aws.amazon.com/sagemaker/latest/dg/feature-store.html
- Pipelines: https://docs.aws.amazon.com/sagemaker/latest/dg/pipelines.html
- Canvas: https://docs.aws.amazon.com/sagemaker/latest/dg/canvas.html
- AgentCore: documentação: https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/what-is-bedrock-agentcore.html
- AgentCore: perguntas frequentes: https://aws.amazon.com/bedrock/agentcore/faqs/
- Strands Agents: documentação: https://strandsagents.com/latest/
- Strands: protocolos abertos: https://aws.amazon.com/blogs/opensource/open-protocols-with-the-strands-agents-sdk/
- Kiro: documentação: https://kiro.dev/docs/
- Amazon Nova: https://aws.amazon.com/nova/
- AWS Transform: documentação: https://docs.aws.amazon.com/transform/
- AWS AI responsável: https://aws.amazon.com/ai/responsible-ai/
- Generative AI Security Scoping Matrix: https://aws.amazon.com/blogs/security/securing-generative-ai-an-introduction-to-the-generative-ai-security-scoping-matrix/
- Classes S3: https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html
- PrivateLink: https://aws.amazon.com/privatelink/
- Visão geral dos serviços AWS: https://docs.aws.amazon.com/whitepapers/latest/aws-overview/introduction.html

### [P] Analytics — produto e cobrança

- AWS Data Exchange: https://aws.amazon.com/data-exchange/pricing/
- Amazon EMR: https://aws.amazon.com/emr/pricing/
- AWS Glue: https://aws.amazon.com/glue/pricing/
- AWS Glue DataBrew: https://aws.amazon.com/glue/databrew/pricing/
- AWS Lake Formation: https://aws.amazon.com/lake-formation/pricing/
- Amazon OpenSearch Service: https://aws.amazon.com/opensearch-service/pricing/
- Amazon Quick: https://aws.amazon.com/quick/
- Amazon Redshift: https://aws.amazon.com/redshift/pricing/

### [P] Cloud Financial Management — produto e cobrança

- AWS Budgets: https://aws.amazon.com/aws-cost-management/aws-budgets/pricing/
- AWS Cost Explorer: https://aws.amazon.com/aws-cost-management/aws-cost-explorer/pricing/

### [P] Compute — produto e cobrança

- Amazon EC2: https://aws.amazon.com/ec2/pricing/
- AWS Lambda: https://aws.amazon.com/lambda/pricing/

### [P] Containers — produto e cobrança

- Amazon Elastic Container Service (Amazon ECS): https://aws.amazon.com/ecs/pricing/
- Amazon Elastic Kubernetes Service (Amazon EKS): https://aws.amazon.com/eks/pricing/

### [P] Database — produto e cobrança

- Amazon Aurora: https://aws.amazon.com/rds/aurora/pricing/
- Amazon DocumentDB (with MongoDB compatibility): https://aws.amazon.com/documentdb/pricing/
- Amazon DynamoDB: https://aws.amazon.com/dynamodb/pricing/
- Amazon ElastiCache: https://aws.amazon.com/elasticache/pricing/
- Amazon Neptune: https://aws.amazon.com/neptune/pricing/
- Amazon RDS: https://aws.amazon.com/rds/pricing/

### [P] Developer Tools — produto e cobrança

- Kiro: https://kiro.dev/pricing/
- Strands Agents: https://docs.aws.amazon.com/prescriptive-guidance/latest/agentic-ai-frameworks/strands-agents.html

### [P] Machine Learning — produto e cobrança

- Amazon Bedrock: https://aws.amazon.com/bedrock/pricing/
- Amazon Bedrock AgentCore: https://aws.amazon.com/bedrock/agentcore/pricing/
- Amazon Comprehend: https://aws.amazon.com/comprehend/pricing/
- Amazon Lex: https://aws.amazon.com/lex/pricing/
- Amazon Nova: https://aws.amazon.com/bedrock/pricing/
- Amazon Personalize: https://aws.amazon.com/personalize/pricing/
- Amazon Polly: https://aws.amazon.com/polly/pricing/
- Amazon Rekognition: https://aws.amazon.com/rekognition/pricing/
- Amazon SageMaker AI: https://aws.amazon.com/sagemaker/ai/pricing/
- Amazon SageMaker JumpStart: https://aws.amazon.com/sagemaker/ai/pricing/
- Amazon Textract: https://aws.amazon.com/textract/pricing/
- Amazon Transcribe: https://aws.amazon.com/transcribe/pricing/
- Amazon Translate: https://aws.amazon.com/translate/pricing/
- AWS Transform: https://aws.amazon.com/transform/pricing/

### [P] Management and Governance — produto e cobrança

- AWS CloudTrail: https://aws.amazon.com/cloudtrail/pricing/
- Amazon CloudWatch: https://aws.amazon.com/cloudwatch/pricing/
- AWS Config: https://aws.amazon.com/config/pricing/
- AWS Trusted Advisor: https://aws.amazon.com/premiumsupport/technology/trusted-advisor/
- AWS Well-Architected Tool: https://aws.amazon.com/well-architected-tool/pricing/

### [P] Networking and Content Delivery — produto e cobrança

- Amazon CloudFront: https://aws.amazon.com/cloudfront/pricing/
- Amazon VPC: https://aws.amazon.com/vpc/pricing/

### [P] Security, Identity, and Compliance — produto e cobrança

- AWS Artifact: https://aws.amazon.com/artifact/pricing/
- AWS Identity and Access Management (IAM): https://aws.amazon.com/iam/pricing/
- Amazon Inspector: https://aws.amazon.com/inspector/pricing/
- AWS Key Management Service (AWS KMS): https://aws.amazon.com/kms/pricing/
- Amazon Macie: https://aws.amazon.com/macie/pricing/
- AWS Secrets Manager: https://aws.amazon.com/secrets-manager/pricing/

### [P] Storage — produto e cobrança

- Amazon S3: https://aws.amazon.com/s3/pricing/
- Amazon S3 Glacier: https://aws.amazon.com/s3/pricing/
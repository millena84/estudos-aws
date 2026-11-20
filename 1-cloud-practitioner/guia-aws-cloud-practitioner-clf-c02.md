# AWS Certified Cloud Practitioner (CLF-C02) — guia de estudos

Referência: guia oficial vigente consultado em 18/11/2026. Este material cobre as 111 entradas da lista oficial publicada, distribuídas em 19 categorias, e os 19 objetivos do exame; a própria AWS diz que o escopo é não exaustivo e pode mudar. “Ponto de prova” indica o que vale saber para reconhecer o serviço, não uma promessa de questão. Este é um exame de fundamentos: não exige codificar, implementar, desenhar arquitetura, diagnosticar problemas ou testar performance. O exame tem 65 perguntas (50 pontuadas, 15 não pontuadas e não identificadas); aprovação a partir de 700 em escala 100–1.000, não necessariamente 70% de acertos. Questão em branco conta como erro; não há penalidade extra por tentar.

## 1. Conteúdo por domínio

### Domínio 1 — Conceitos de nuvem (24%)

- 1.1 Benefícios: alcance global, agilidade, provisionamento rápido, elasticidade e alta disponibilidade. Escalabilidade é a capacidade de crescer; elasticidade é ajustar capacidade à demanda para cima e para baixo. Alta disponibilidade reduz indisponibilidade, mas não garante recuperação de dados.
- 1.2 Well-Architected: excelência operacional (operar e melhorar); segurança (proteger); confiabilidade (resistir e recuperar); eficiência de performance (usar recursos adequados); otimização de custos (entregar valor sem desperdício); sustentabilidade (reduzir impacto ambiental). Exemplo: rightsizing reduz desperdício; sobreviver à perda de uma AZ é confiabilidade.
- 1.3 Adoção e migração: AWS CAF tem seis perspectivas — negócio, pessoas, governança, plataforma, segurança e operações. Busca redução de risco, melhora de ESG, receita e eficiência. Reconheça as 7 estratégias: retire (desativar), retain (manter), rehost (mover como está), relocate (mover plataforma com pouca mudança), repurchase (trocar produto), replatform (ajustar plataforma sem grande reescrita) e refactor/re-architect (redesenhar). Replicar banco com CDC pode reduzir a janela de indisponibilidade.
- 1.4 Economia: custo fixo versus variável, CapEx versus OpEx, custo total de propriedade (inclui pessoas, licenças, datacenter e operação), economias de escala, automação, rightsizing, BYOL versus licença incluída. Nuvem não é automaticamente mais barata: recursos ociosos e transferência influenciam a conta.

### Domínio 2 — Segurança e conformidade (30%)

- 2.1 Responsabilidade compartilhada: AWS protege a infraestrutura **da** nuvem; cliente protege dados, permissões e configurações **na** nuvem. Em EC2 o cliente corrige o SO convidado; em RDS AWS opera a infraestrutura e o SO subjacente, enquanto cliente cuida de dados, acesso e parâmetros; em Lambda AWS opera a plataforma, mas cliente cuida de código, dependências e permissões. Alguns controles são compartilhados em camadas diferentes: patch do host AWS não isenta patch do software do cliente.
- 2.2 Governança e compliance: Artifact para relatórios AWS; verificar Região, setor e serviços elegíveis. Criptografia em repouso versus TLS em trânsito; KMS para chaves e ACM para certificados. CloudTrail = identidade/ação; Config = estado/conformidade; CloudWatch = métricas/logs/alarmes. Relatórios de acesso auxiliam auditoria; GuardDuty, Inspector, Security Hub e Shield têm papéis distintos.
- 2.3 Acesso: menor privilégio, MFA, federação, roles cross-account e credenciais temporárias. Usuários, grupos e roles não são políticas; políticas gerenciadas da AWS, gerenciadas pelo cliente e inline têm escopos distintos. Evite chaves persistentes do root, proteja a recuperação e reserve root para tarefas oficialmente exclusivas, como mudanças específicas de conta; confira exceções para contas-membro com acesso root centralizado. Senhas/chaves são credenciais: use Secrets Manager ou Parameter Store conforme necessidade; não coloque segredos no código.
- 2.4 Serviços e fontes de segurança: WAF filtra HTTP(S), Shield protege contra DDoS, Firewall Manager distribui políticas, GuardDuty detecta ameaças, Trusted Advisor recomenda. Saiba localizar AWS Security Center, AWS Security Blog, Knowledge Center/re:Post e produtos de terceiros no Marketplace.

### Domínio 3 — Tecnologias e serviços de nuvem (34%)

- 3.1 Operação: Console para tarefa pontual; API para interface programática; CLI para terminal/scripts; SDK para código; CloudFormation/IaC para repetição e versionamento. Modelos de implantação: cloud, on-premises e híbrido.
- 3.2 Infraestrutura: Região agrupa AZs isoladas entre si; AZ contém um ou mais datacenters; ponto de presença na borda aproxima entrega do usuário. Multi-AZ mitiga falha zonal; multi-Região pode atender continuidade, DR, latência ou soberania. Nenhum dos dois, por si só, substitui backup.
- 3.3 Computação: famílias EC2; ECS/EKS; Lambda/Fargate; elasticidade por Auto Scaling e distribuição por Elastic Load Balancing. EC2 é VM: oferece controle de SO; serviço gerenciado oferece menos controle em troca de menos operação. ELB distribui carga; Auto Scaling altera capacidade.
- 3.4 Bancos: EC2 autogerenciado versus gerenciado; RDS/Aurora relacionais, DynamoDB NoSQL, ElastiCache em memória. DMS move dados; SCT ajuda converter esquemas. DocumentDB é documentos; Neptune é grafos.
- 3.5 Rede: VPC, sub-redes, rotas, gateways, SG e NACL; Route 53 para DNS; VPN versus Direct Connect. Inspector avalia exposição e vulnerabilidade de workloads suportados, não substitui controles da rede.
- 3.6 Storage: objetos S3; blocos EBS/instance store; arquivos EFS/FSx; classes S3 e regras de ciclo de vida (lifecycle); integração local via Storage Gateway; políticas centralizadas via Backup. Instance store é armazenamento local temporário ligado ao host, sem persistência após certos eventos como stop/terminate.
- 3.7 IA/ML e analytics: reconhecer tarefas de SageMaker AI, Lex e APIs prontas; distinguir SQL sobre S3 (Athena), streaming (Kinesis), ETL/catálogo (Glue) e BI (Quick).
- 3.8 Demais categorias: mensageria/alerta e orquestração; Connect/SES; AWS Support; ferramentas de CI/CD, CLI e tracing; desktop/aplicação/browser remoto; Amplify; IoT Core. Identificar o serviço certo pelo requisito, não só pela sigla.

### Domínio 4 — Cobrança, preços e suporte (12%)

- 4.1 On-Demand: sem compromisso, para uso imprevisível. Spot: capacidade ociosa sujeita a interrupção, para cargas tolerantes (lote, workers). RI: desconto por configuração/escopo elegível, normalmente 1 ou 3 anos; Standard e Convertible diferem na flexibilidade, e RI zonal pode reservar capacidade com atributos correspondentes. Desconto de RI regional não equivale a capacidade reservada; flexibilidade de tamanho depende de condições. Savings Plans: compromisso monetário por hora de 1 ou 3 anos; Compute Savings Plans alcança EC2, Fargate e Lambda; EC2 Instance Savings Plans é mais restrito. Nenhum Savings Plan reserva capacidade. Capacity Reservation: reserva capacidade na AZ, pode cobrar mesmo ociosa; não é desconto por si só. Dedicated Host: servidor físico alocado com visibilidade do host e benefícios para certos BYOL; Dedicated Instances: isolamento físico de outras contas sem o mesmo controle do host. Em Organizations, descontos elegíveis podem ser compartilhados na família de cobrança conforme configuração; não presuma compartilhamento indiscriminado nem confunda desconto com reserva física.
- 4.1 Transferência e storage: entrada da internet geralmente não tem cobrança de transferência, mas serviços intermediários/processamento podem cobrar. Saída para internet, tráfego entre Regiões e, dependendo do caminho e dos serviços, entre AZs podem custar. Preço depende de classe, Região, requisições, recuperação e retenção mínima. Exemplo: migrar dados consultados todos os dias para Deep Archive apenas pelo preço por GB pode aumentar custo e inviabilizar a latência necessária.
- 4.2 Calculator estima antes de contratar; Explorer analisa realizado e previsões; Budgets envia alertas e pode executar ações configuradas; CUR/Data Exports fornece linhas detalhadas. Organizations consolida cobrança; tags de alocação, AWS-generated ou do usuário, precisam estar disponíveis/ativadas conforme a modalidade para uso nos relatórios. Nem todo custo será atribuível por tag.
- 4.3 Suporte: Basic (incluído; conta, cobrança e materiais de autoatendimento, sem suporte técnico pago); Business Support+ (engenheiros 24×7, menos de 30 min para caso crítico elegível, mínimo publicado de US$ 29/mês por conta); Enterprise Support (TAM designado, até 15 min em caso crítico de produção, mínimo publicado de US$ 5.000/mês); Unified Operations (orientação e acompanhamento mais próximos para operações críticas; conferir contrato e comparação oficial). Não misture esses planos com Developer, Business ou Enterprise On-Ramp de materiais antigos: AWS documenta transição até 1º de janeiro de 2027, com exceções para GovCloud (US). Tempo de resposta inicial não é prazo de resolução.
- 4.3 Recursos e parceiros: Support Center abre casos; Knowledge Center/re:Post responde dúvidas; Prescriptive Guidance oferece guias e padrões; documentação, whitepapers e blogs são fontes oficiais; Trust & Safety recebe denúncias de abuso de recursos AWS. Health Dashboard/API comunica eventos; Trusted Advisor sugere melhorias. APN reúne fornecedores independentes de software (ISVs) e integradores; parceiros têm acesso a oportunidades de treinamento, certificação e eventos conforme programa. Marketplace auxilia compra, gestão de custos, governança e direitos de uso. AWS Professional Services apoia execução de projetos; Solutions Architects orientam decisões técnicas.

## 2. Catálogo oficial de serviços e funcionalidades

As categorias abaixo mantêm os nomes do guia. Cobrança descreve a unidade predominante e opções úteis para estudo, não uma cotação: Região, edição, descontos, recursos associados e alterações de produto podem mudar o total. Os links por serviço estão na seção final. A lista oficial inclui a família AWS VPN e seus dois tipos em linhas próprias; também lista S3 e S3 Glacier separadamente.


### Analytics


#### Amazon Athena

- O que é: SQL serverless sobre dados no S3.
- Quando usar: Consulta exploratória de logs ou data lake.
- Quando não usar: Não para transações de aplicação: RDS.
- Cobrança: Dados examinados por consulta ou capacidade provisionada.
- Ponto de prova e pegadinha: Parquet e partições reduzem bytes lidos; Glue cataloga, Athena consulta.


#### Amazon EMR

- O que é: Plataforma para Spark, Hadoop e outros frameworks distribuídos.
- Quando usar: Processar grandes volumes com Spark/PySpark e ajustar o ambiente.
- Quando não usar: Não para SQL avulso no S3: Athena.
- Cobrança: Taxa EMR mais infraestrutura no modo cluster; vCPU, memória e armazenamento conforme modo Serverless.
- Ponto de prova e pegadinha: EMR executa frameworks; não é data warehouse.


#### AWS Glue

- O que é: Integração serverless de dados com ETL e catálogo.
- Quando usar: Descobrir esquemas e transformar dados para analytics.
- Quando não usar: Não para dashboard ou consulta ad hoc: Quick ou Athena.
- Cobrança: Capacidade de processamento (DPU-tempo); catálogo e recursos conforme uso.
- Ponto de prova e pegadinha: Crawler descobre metadados; Data Catalog não armazena os dados; ETL é extrair, transformar e carregar.


#### Amazon Kinesis

- O que é: Família de serviços de streaming.
- Quando usar: Ingerir telemetria continuamente para processamento em tempo real.
- Quando não usar: Não para fila de tarefas com um trabalhador por mensagem: SQS.
- Cobrança: Data Streams sob demanda por volume e métricas do modo; provisionado por shard e uso; outros produtos têm métricas próprias.
- Ponto de prova e pegadinha: Data Streams permite retenção e releitura; Firehose é entrega gerenciada, não o mesmo recurso.


#### Amazon OpenSearch Service

- O que é: Busca e analytics de texto e logs.
- Quando usar: Indexar logs, oferecer busca textual e visualizar eventos.
- Quando não usar: Não como banco transacional primário.
- Cobrança: Instâncias e armazenamento ou unidades OCU e armazenamento no Serverless.
- Ponto de prova e pegadinha: Indexar para buscar é diferente de consultar arquivos com Athena.


#### Amazon Quick

- O que é: Plataforma de análise e BI; QuickSight é o nome que você pode encontrar em materiais de BI anteriores.
- Quando usar: Publicar dashboards e compartilhar indicadores.
- Quando não usar: Não para ETL nem para substituir o warehouse.
- Cobrança: Assinaturas, capacidade ou consumo conforme componente e edição.
- Ponto de prova e pegadinha: Visualiza dados de fontes como Redshift e Athena; não é o motor ETL.


#### Amazon Redshift

- O que é: Data warehouse analítico colunar.
- Quando usar: Agregações SQL sobre grandes históricos e BI corporativo.
- Quando não usar: Não para cadastro transacional: RDS ou DynamoDB.
- Cobrança: Nós provisionados ou RPU-tempo no Serverless; armazenamento separado quando aplicável.
- Ponto de prova e pegadinha: OLAP analisa muitas linhas; OLTP opera transações pequenas; Spectrum consulta dados externos no S3.


### Application Integration


#### Amazon EventBridge

- O que é: Barramento e roteador de eventos baseado em regras.
- Quando usar: Receber eventos de serviços, aplicações e SaaS e encaminhar por conteúdo.
- Quando não usar: Não para backlog com consumidores fazendo polling: SQS.
- Cobrança: Eventos conforme origem, volume e tamanho; Scheduler e Pipes têm métricas próprias.
- Ponto de prova e pegadinha: Regra filtra e envia a destinos; não é fila nem orquestrador de estados.


#### Amazon Simple Notification Service (Amazon SNS)

- O que é: Mensageria publish/subscribe por tópicos.
- Quando usar: Distribuir um evento a vários assinantes ou notificar.
- Quando não usar: Não como fila de trabalho para polling: SQS.
- Cobrança: Solicitações, entregas e transferência conforme protocolo; SMS tem preço próprio.
- Ponto de prova e pegadinha: Fan-out SNS → múltiplas filas SQS; push não é polling.


#### Amazon Simple Queue Service (Amazon SQS)

- O que é: Fila gerenciada.
- Quando usar: Desacoplar produtor e consumidor e absorver picos.
- Quando não usar: Não para notificar diversos destinos diretamente: SNS.
- Cobrança: Solicitações; volume é influenciado por tamanho e batching.
- Ponto de prova e pegadinha: Standard: pelo menos uma entrega e ordem de melhor esforço; FIFO: ordem por grupo e deduplicação; DLQ recebe falhas repetidas.


#### AWS Step Functions

- O que é: Orquestração por máquinas de estados.
- Quando usar: Encadear serviços com decisões, paralelismo, retries e tratamento de erros.
- Quando não usar: Não para armazenar um backlog nem executar lógica no lugar do Lambda.
- Cobrança: Standard por transição; Express por execuções e duração/memória.
- Ponto de prova e pegadinha: Coordena as etapas; Lambda pode executar uma etapa.


### Business Applications


#### Amazon Connect

- O que é: Central de atendimento em nuvem.
- Quando usar: Telefonia, chat, roteamento e filas de atendimento.
- Quando não usar: Não para disparar e-mail transacional em massa: SES.
- Cobrança: Uso por canal e funcionalidade; voz e telefonia têm componentes próprios.
- Ponto de prova e pegadinha: Contact center é diferente de serviço de e-mail ou chatbot isolado.


#### Amazon Simple Email Service (Amazon SES)

- O que é: Envio e recebimento gerenciado de e-mail.
- Quando usar: Enviar confirmações, avisos e campanhas ou processar e-mail recebido.
- Quando não usar: Não para hospedar caixas postais ou enviar SMS.
- Cobrança: Mensagens, dados/anexos e extras como IP dedicado.
- Ponto de prova e pegadinha: Identidades verificadas e sandbox de envio; SES é e-mail, SNS distribui notificações.


### Cloud Financial Management


#### AWS Budgets

- O que é: Orçamentos e alertas de custo, uso e compromissos.
- Quando usar: Avisar quando custo previsto ou realizado atingir limites.
- Quando não usar: Não para estimativa prévia de nova arquitetura: Pricing Calculator.
- Cobrança: Orçamentos de monitoramento sem taxa; ações e relatórios têm regras próprias.
- Ponto de prova e pegadinha: Alerta não é bloqueio automático; ações precisam ser configuradas.


#### AWS Cost and Usage Reports

- O que é: Exportação detalhada de dados de cobrança e consumo (CUR/CUR 2.0).
- Quando usar: Investigar custo por conta, recurso ou tag com SQL/BI.
- Quando não usar: Não para receber alerta imediato ou simplesmente navegar pela tendência.
- Cobrança: Sem taxa pela geração padrão; S3 e consultas podem custar.
- Ponto de prova e pegadinha: Relatório detalhado não é a visualização do Cost Explorer.


#### AWS Cost Explorer

- O que é: Visualização e análise de custos e uso.
- Quando usar: Filtrar histórico, agrupar gastos e analisar previsões e compromissos.
- Quando não usar: Não para impor limites nem substituir exportação granular.
- Cobrança: Interface padrão sem taxa; API e granularidades opcionais podem ser cobradas.
- Ponto de prova e pegadinha: Explorer analisa; Budgets alerta; Calculator estima.


#### AWS Marketplace

- O que é: Catálogo para descobrir e contratar software, dados e serviços de terceiros.
- Quando usar: Comprar AMI, SaaS ou soluções de parceiros com governança de compras.
- Quando não usar: Não para provisionar somente os produtos internos aprovados: Service Catalog.
- Cobrança: Modelo do fornecedor: assinatura, consumo, contrato ou BYOL; infraestrutura pode ser separada.
- Ponto de prova e pegadinha: Compra de terceiros pode aparecer na fatura AWS; governança e direitos de uso não são o mesmo que IAM.


### Compute


#### AWS Batch

- O que é: Agendamento gerenciado de jobs em lote.
- Quando usar: Enfileirar e paralelizar simulações e processamento assíncrono.
- Quando não usar: Não para servir uma API interativa com baixa latência.
- Cobrança: Sem taxa adicional pelo Batch; paga EC2, Fargate e recursos usados.
- Ponto de prova e pegadinha: Job queue e compute environment; Batch agenda, não é runtime.


#### Amazon EC2

- O que é: Máquinas virtuais configuráveis.
- Quando usar: Controle do SO, agentes, software legado ou computação especializada.
- Quando não usar: Não quando serviço gerenciado reduz a operação e atende aos requisitos.
- Cobrança: On-Demand por tempo; Spot; RI ou Savings Plans para descontos; armazenamento e transferência separados.
- Ponto de prova e pegadinha: Geral, computação, memória, armazenamento ou aceleradores; cliente administra SO convidado; instance store é temporário.


#### AWS Elastic Beanstalk

- O que é: Plataforma para implantar apps administrando componentes de infraestrutura.
- Quando usar: Publicar app web em runtime suportado sem montar tudo manualmente.
- Quando não usar: Não para eventos curtos sem servidores: Lambda; nem controle total do deploy.
- Cobrança: Sem taxa Beanstalk; paga EC2, ELB, armazenamento etc..
- Ponto de prova e pegadinha: Você envia o código; Beanstalk provisiona e gerencia o ambiente, mas recursos existem e são cobrados.


#### Amazon Lightsail

- O que é: Pacotes simplificados de VPS e serviços associados.
- Quando usar: Site pequeno, WordPress ou protótipo com pacote previsível.
- Quando não usar: Não para arquitetura que exige grande variedade de recursos e controle fino.
- Cobrança: Pacotes mensais com franquias; adicionais e excedentes conforme produto.
- Ponto de prova e pegadinha: É simplificado, não gratuito e não é equivalente a todo o catálogo EC2.


#### AWS Outposts

- O que é: Infraestrutura AWS instalada no local do cliente.
- Quando usar: Baixa latência local e requisitos de processamento no local.
- Quando não usar: Não quando uma Região pública cumpre os requisitos.
- Cobrança: Contrato de capacidade e configuração; modalidades e serviços adicionais variam.
- Ponto de prova e pegadinha: AWS no local do cliente, integrado à Região; não é uma nova Região.


### Containers


#### Amazon Elastic Container Registry (Amazon ECR)

- O que é: Registro de imagens de contêiner.
- Quando usar: Armazenar, versionar e distribuir imagens para deploy.
- Quando não usar: Não para executar ou orquestrar contêineres.
- Cobrança: Armazenamento, transferência aplicável e extras como escaneamento avançado.
- Ponto de prova e pegadinha: ECR guarda a imagem; ECS/EKS executam a aplicação com capacidade de computação.


#### Amazon Elastic Container Service (Amazon ECS)

- O que é: Orquestrador nativo da AWS.
- Quando usar: Agendar contêineres sem exigir Kubernetes.
- Quando não usar: Não quando a API e o ecossistema Kubernetes são requisitos: EKS.
- Cobrança: Modelo padrão em EC2/Fargate cobra a capacidade subjacente; opções como ECS Anywhere e ECS Managed Instances podem adicionar taxas.
- Ponto de prova e pegadinha: Task definition descreve o contêiner; service mantém réplicas; EC2 ou Fargate executa.


#### Amazon Elastic Kubernetes Service (Amazon EKS)

- O que é: Kubernetes gerenciado.
- Quando usar: Operar workloads que precisam da API e do ecossistema Kubernetes.
- Quando não usar: Não se não há requisito Kubernetes e ECS é suficiente.
- Cobrança: Taxa de cluster, inclusive conforme suporte à versão, mais capacidade e extras conforme modo.
- Ponto de prova e pegadinha: AWS gerencia o plano de controle; pods rodam em nós ou Fargate nas configurações suportadas.


### Customer Enablement


#### AWS Support

- O que é: Orientação e atendimento AWS conforme plano.
- Quando usar: Abrir chamados e obter assistência alinhada à criticidade.
- Quando não usar: Não para terceirizar toda a operação diária ou reportar abuso de terceiros.
- Cobrança: Basic incluído; planos pagos conforme mínimo, consumo e contrato.
- Ponto de prova e pegadinha: Support Center abre casos; TAM é do Enterprise; Trusted Advisor é ferramenta de recomendações.


### Database


#### Amazon Aurora

- O que é: Banco relacional AWS compatível com MySQL ou PostgreSQL.
- Quando usar: SQL transacional com arquitetura gerenciada e alta disponibilidade.
- Quando não usar: Não para SQL Server, Oracle ou grafo.
- Cobrança: Instâncias ou ACU-tempo; armazenamento, backup e I/O conforme configuração.
- Ponto de prova e pegadinha: Aurora integra a família RDS; Serverless ajusta capacidade, mas não implica custo zero.


#### Amazon DocumentDB

- O que é: Banco de documentos compatível com APIs MongoDB.
- Quando usar: Aplicações que persistem documentos e atendem à matriz de compatibilidade.
- Quando não usar: Não presumir compatibilidade integral com MongoDB nem escolher para joins relacionais.
- Cobrança: Instâncias ou capacidade serverless conforme oferta; armazenamento, I/O e backup conforme configuração.
- Ponto de prova e pegadinha: Compatível com APIs não significa implementar todas as funcionalidades do MongoDB.


#### Amazon DynamoDB

- O que é: NoSQL gerenciado de chave-valor e documentos.
- Quando usar: Leituras rápidas e previsíveis por chaves em alta escala.
- Quando não usar: Não para joins e consultas relacionais ad hoc.
- Cobrança: On-demand por requisições ou capacidade provisionada; armazenamento e extras.
- Ponto de prova e pegadinha: Chave de partição, índices, TTL, Global Tables; modelar a partir dos padrões de acesso.


#### Amazon ElastiCache

- O que é: Armazenamento em memória gerenciado, usualmente usado como cache.
- Quando usar: Acelerar leituras e guardar sessões/dados quentes.
- Quando não usar: Não escolher como substituto automático do banco durável de referência.
- Cobrança: Nós ou, no serverless, armazenamento e capacidade de processamento.
- Ponto de prova e pegadinha: Cache reduz latência e carga do banco; Valkey, Redis OSS e Memcached conforme oferta.


#### Amazon Neptune

- O que é: Banco de grafos gerenciado.
- Quando usar: Consultar redes de relacionamentos, como vínculos entre contas e dispositivos.
- Quando não usar: Não para CRUD simples por chave ou warehouse SQL.
- Cobrança: Instâncias ou capacidade serverless, armazenamento e I/O conforme configuração.
- Ponto de prova e pegadinha: Vértices e arestas; caminho e vizinhança são sinais de questão de grafo.


#### Amazon RDS

- O que é: Serviço gerenciado para bancos relacionais.
- Quando usar: SQL e transações com menos operação de banco.
- Quando não usar: Não quando é indispensável controle total do SO ou engine não suportado: EC2.
- Cobrança: Instância, armazenamento, I/O e backup; opções reservadas para uso estável.
- Ponto de prova e pegadinha: Multi-AZ para disponibilidade; réplicas de leitura para escalar leituras. Clusters Multi-AZ podem ter leitores; não generalize.


### Developer Tools


#### AWS CLI

- O que é: Cliente de linha de comando para APIs AWS.
- Quando usar: Automatizar operações em scripts ou terminal.
- Quando não usar: Não para declarar estado desejado da infraestrutura: CloudFormation.
- Cobrança: CLI sem taxa; chamadas e recursos seguem o preço do serviço.
- Ponto de prova e pegadinha: CLI é interface; SDK integra código; nenhuma das duas concede permissões.


#### AWS CodeBuild

- O que é: Build e testes gerenciados.
- Quando usar: Compilar, testar e gerar artefato em CI.
- Quando não usar: Não para definir sozinho o fluxo de release inteiro: CodePipeline.
- Cobrança: Tempo de build por tipo de ambiente; modalidades reservadas podem variar.
- Ponto de prova e pegadinha: CodeBuild compila e testa; CodePipeline coordena.


#### AWS CodePipeline

- O que é: Orquestração de entrega contínua.
- Quando usar: Ligar origem, build, aprovação e deploy.
- Quando não usar: Não como compilador nem runtime da aplicação.
- Cobrança: Por pipeline ativo ou duração de ações, conforme tipo; serviços chamados à parte.
- Ponto de prova e pegadinha: Um pipeline pode chamar CodeBuild; pipeline não substitui um build.


#### AWS X-Ray

- O que é: Rastreamento distribuído de requisições.
- Quando usar: Descobrir em qual serviço uma requisição fica lenta ou falha.
- Quando não usar: Não para auditoria de chamadas AWS: CloudTrail.
- Cobrança: Traces gravados, recuperados e analisados conforme uso.
- Ponto de prova e pegadinha: Trace mostra o caminho de uma requisição por serviços; métricas e logs são complementares.


### End User Computing


#### Amazon AppStream 2.0

- O que é: Streaming de aplicações e desktops; também encontrado como Amazon WorkSpaces Applications.
- Quando usar: Entregar aplicações remotamente sem instalá-las no dispositivo.
- Quando não usar: Não para entregar um desktop pessoal persistente quando WorkSpaces atende.
- Cobrança: Capacidade da frota e taxas de usuário/licença conforme tipo.
- Ponto de prova e pegadinha: Pista típica: streaming de uma aplicação; não confundir com navegador isolado.


#### Amazon WorkSpaces

- O que é: Desktops virtuais gerenciados.
- Quando usar: Fornecer ambiente de trabalho remoto aos colaboradores.
- Quando não usar: Não para acesso só a um portal web ou só a um aplicativo.
- Cobrança: Pacotes mensais ou por hora com componente fixo, conforme oferta.
- Ponto de prova e pegadinha: Desktop completo; persistência depende da modalidade.


#### Amazon WorkSpaces Secure Browser

- O que é: Navegador remoto isolado.
- Quando usar: Acessar portais e aplicações web sem entregar desktop completo.
- Quando não usar: Não para apps nativos fora do navegador.
- Cobrança: Usuário ativo mensal e sessões/horas adicionais conforme franquia.
- Ponto de prova e pegadinha: Navegador remoto não é VPN nem desktop completo.


### Frontend Web and Mobile


#### AWS Amplify

- O que é: Ferramentas e hospedagem para apps web/mobile.
- Quando usar: Publicar frontend com deploy por Git e integrar backend.
- Quando não usar: Não como plataforma genérica para VMs personalizadas.
- Cobrança: Minutos de build, armazenamento, tráfego e SSR conforme uso; backend separado.
- Ponto de prova e pegadinha: Amplify Hosting é frontend; não confundir com Beanstalk para ambiente de aplicação.


### Internet of Things (IoT)


#### AWS IoT Core

- O que é: Conexão e roteamento gerenciados para dispositivos IoT.
- Quando usar: Receber telemetria autenticada de sensores e enviar comandos.
- Quando não usar: Não como banco histórico ou data warehouse.
- Cobrança: Conectividade, mensagens, regras e Device Shadow conforme uso.
- Ponto de prova e pegadinha: MQTT, registro e Shadow: estado digital do dispositivo, não analytics histórico.


### Machine Learning


#### Amazon Comprehend

- O que é: Processamento de linguagem natural para texto.
- Quando usar: Extrair entidades, tópicos e sentimento de texto existente.
- Quando não usar: Não para áudio bruto ou OCR.
- Cobrança: Unidades de texto e recursos de treinamento/inferência conforme modo.
- Ponto de prova e pegadinha: Comprehend interpreta; Transcribe converte fala em texto.


#### Amazon Lex

- O que é: Interfaces conversacionais de voz e texto.
- Quando usar: Chatbot para capturar intenção e parâmetros.
- Quando não usar: Não para síntese de voz avulsa: Polly.
- Cobrança: Requisições de texto/voz ou modalidade conversacional.
- Ponto de prova e pegadinha: Intenção é o objetivo; slots são parâmetros; Connect é a central de atendimento.


#### Amazon Polly

- O que é: Síntese de fala.
- Quando usar: Ler notícias, mensagens e respostas em voz alta.
- Quando não usar: Não para transcrever gravações: Transcribe.
- Cobrança: Caracteres convertidos, variando pelo tipo de voz.
- Ponto de prova e pegadinha: Texto → voz.


#### Amazon Q

- O que é: Família de assistentes generativos AWS.
- Quando usar: Assistência a desenvolvedores ou respostas sobre dados corporativos conforme a edição.
- Quando não usar: Não para treinar modelo próprio: SageMaker AI.
- Cobrança: Assinaturas e limites/consumo conforme edição; integrações e indexação podem custar.
- Ponto de prova e pegadinha: Q Developer auxilia desenvolvimento; Q Business responde sobre conteúdo empresarial conforme acesso.


#### Amazon Rekognition

- O que é: Análise de imagens e vídeo.
- Quando usar: Detectar objetos, cenas ou moderar imagens e vídeos.
- Quando não usar: Não para extrair formulários e tabelas: Textract.
- Cobrança: Imagens, minutos de vídeo e recursos opcionais.
- Ponto de prova e pegadinha: Reconhecimento visual não é OCR estruturado de documentos.


#### Amazon SageMaker AI

- O que é: Plataforma para criar, treinar e implantar modelos de ML.
- Quando usar: Treinar modelo próprio e administrar seu ciclo de vida.
- Quando não usar: Não quando uma API pronta resolve com menos operação.
- Cobrança: Ambientes, treinamento, inferência, armazenamento e recursos conforme uso.
- Ponto de prova e pegadinha: Treinar é aprender; inferir é usar o modelo treinado; endpoint provisionado pode custar ocioso.


#### Amazon Textract

- O que é: OCR e extração estruturada de documentos.
- Quando usar: Extrair texto, pares chave-valor e tabelas de documentos digitalizados.
- Quando não usar: Não para transcrever áudio ou traduzir.
- Cobrança: Páginas e tipo de API, como texto, formulário ou tabela.
- Ponto de prova e pegadinha: Documento estruturado aponta para Textract; imagem genérica, para Rekognition.


#### Amazon Transcribe

- O que é: Reconhecimento automático de fala.
- Quando usar: Gerar texto de áudio ao vivo ou gravado.
- Quando não usar: Não para gerar voz nem traduzir texto.
- Cobrança: Duração de áudio e modalidade.
- Ponto de prova e pegadinha: Voz → texto; Polly faz o inverso.


#### Amazon Translate

- O que é: Tradução automática de texto.
- Quando usar: Traduzir conteúdo entre idiomas.
- Quando não usar: Não converte diretamente uma gravação em transcrição nem avalia sentimento.
- Cobrança: Caracteres processados, conforme modalidade.
- Ponto de prova e pegadinha: Áudio em outro idioma pode exigir Transcribe seguido de Translate.


### Management and Governance


#### AWS Auto Scaling

- O que é: Dimensionamento automático de capacidade.
- Quando usar: Aumentar e reduzir recursos conforme demanda.
- Quando não usar: Não para distribuir requisições: use ELB como complemento.
- Cobrança: Sem taxa adicional pela função padrão; recursos e métricas associadas podem custar.
- Ponto de prova e pegadinha: Elasticidade: scale out adiciona unidades, scale in remove; ALB distribui, não cria instâncias.


#### AWS CloudFormation

- O que é: Infraestrutura como código declarativa.
- Quando usar: Repetir provisionamento de ambientes por templates e stacks.
- Quando não usar: Não para observar métricas ou rodar tarefas operacionais pontuais.
- Cobrança: Sem taxa adicional para uso padrão com recursos AWS; extensões específicas podem custar; recursos provisionados à parte.
- Ponto de prova e pegadinha: Templates descrevem estado, stacks agrupam recursos e change sets mostram mudanças previstas.


#### AWS CloudTrail

- O que é: Auditoria de atividade de contas e chamadas de API.
- Quando usar: Saber quem alterou um recurso e quando.
- Quando não usar: Não para CPU, latência e alarmes: CloudWatch.
- Cobrança: Histórico padrão de eventos de gerenciamento por 90 dias sem taxa; eventos, cópias e Lake conforme modalidade.
- Ponto de prova e pegadinha: Quem fez o quê; data events não são automaticamente equivalentes ao histórico de gerenciamento.


#### Amazon CloudWatch

- O que é: Observabilidade por métricas, logs e alarmes.
- Quando usar: Monitorar CPU, latência, erros, aplicações e acionar alertas.
- Quando não usar: Não para identificar sozinho quem fez uma chamada de API: CloudTrail.
- Cobrança: Métricas, logs, consultas, alarmes e dashboards conforme uso.
- Ponto de prova e pegadinha: Métricas mostram comportamento; logs registram eventos; alarme reage a condições.


#### AWS Compute Optimizer

- O que é: Recomendações de dimensionamento com base no uso.
- Quando usar: Encontrar instâncias e outros recursos super ou subdimensionados.
- Quando não usar: Não para escalar recursos em tempo real.
- Cobrança: Recomendações padrão sem taxa; métricas aprimoradas opcionais cobradas.
- Ponto de prova e pegadinha: Recomendar não é aplicar; rightsizing não é comprar desconto.


#### AWS Config

- O que é: Inventário, histórico e avaliação de configurações.
- Quando usar: Detectar se um recurso ficou fora da política de configuração.
- Quando não usar: Não para saber qual identidade chamou uma API: CloudTrail.
- Cobrança: Itens registrados, avaliações de regras e de conformance packs.
- Ponto de prova e pegadinha: O que mudou e se está conforme; regra detectiva não é bloqueio automático.


#### AWS Control Tower

- O que é: Configuração e governança de ambiente multiaccount.
- Quando usar: Montar landing zone e controles padronizados.
- Quando não usar: Não para compras de terceiros nem somente consolidar faturas.
- Cobrança: Sem taxa adicional do serviço; serviços habilitados custam conforme uso.
- Ponto de prova e pegadinha: Usa Organizations; landing zone é a fundação multiaccount, não uma VPC.


#### AWS Health Dashboard

- O que é: Visibilidade de eventos de serviço e eventos que afetam a conta.
- Quando usar: Investigar indisponibilidade ou manutenção comunicada pela AWS.
- Quando não usar: Não para monitorar métricas da aplicação: CloudWatch.
- Cobrança: Dashboard sem taxa direta; acesso ao Health API depende de elegibilidade/plano.
- Ponto de prova e pegadinha: Visão pública versus eventos específicos da conta; Health não é Trusted Advisor.


#### AWS License Manager

- O que é: Controle e rastreamento de licenças.
- Quando usar: Gerir elegibilidade, uso e limites de BYOL.
- Quando não usar: Não para comprar licenças ou substituir revisão contratual.
- Cobrança: Funções padrão sem taxa adicional; assinaturas e recursos subjacentes podem custar.
- Ponto de prova e pegadinha: BYOL reaproveita licença elegível; licença incluída vem com o preço da oferta.


#### AWS Management Console

- O que é: Interface web de administração AWS.
- Quando usar: Explorar ou executar operações manuais pontuais.
- Quando não usar: Não para repetibilidade e versionamento: IaC.
- Cobrança: Sem taxa da interface; recursos e chamadas conforme serviço.
- Ponto de prova e pegadinha: Console, CLI e SDK podem operar os mesmos recursos respeitando IAM.


#### AWS Organizations

- O que é: Estrutura e governança central de contas.
- Quando usar: Organizar OUs, consolidar cobrança e limitar permissões com SCPs.
- Quando não usar: Não para conceder permissões individuais ou compartilhar recursos diretamente.
- Cobrança: Sem taxa adicional; serviços integrados podem ser cobrados.
- Ponto de prova e pegadinha: SCP define teto, não concede acesso; conta de gerenciamento não é limitada pelas SCPs.


#### AWS Service Catalog

- O que é: Catálogo privado de produtos de TI aprovados.
- Quando usar: Permitir provisionamento padronizado por autosserviço.
- Quando não usar: Não para descobrir ofertas de fornecedores: Marketplace.
- Cobrança: Modelo conforme a oferta de provisionamento; recursos provisionados são cobrados separadamente.
- Ponto de prova e pegadinha: Portfólios e produtos aprovados não são a mesma coisa que Marketplace.


#### Service Quotas

- O que é: Consulta e gestão de limites de serviço.
- Quando usar: Ver cota regional ou solicitar aumento ajustável.
- Quando não usar: Não para aumentar capacidade automaticamente ou limitar orçamento.
- Cobrança: Sem taxa adicional de gestão; recursos consumidos são cobrados.
- Ponto de prova e pegadinha: Aumentar cota não reserva capacidade; nem toda cota é ajustável.


#### AWS Systems Manager

- O que é: Operações centralizadas de recursos gerenciados.
- Quando usar: Inventário, patches, comandos, sessões e parâmetros.
- Quando não usar: Não para declarar infraestrutura inteira: CloudFormation.
- Cobrança: Vários recursos incluídos; parâmetros avançados, throughput e outros recursos opcionais podem custar.
- Ponto de prova e pegadinha: Patch Manager, Session Manager, Run Command e Parameter Store; Secrets Manager é voltado ao ciclo de vida de segredos.


#### AWS Trusted Advisor

- O que é: Recomendações de boas práticas.
- Quando usar: Identificar oportunidades de custo, segurança, desempenho e outros riscos.
- Quando não usar: Não para monitoramento em tempo real nem execução automática de correções.
- Cobrança: Acesso a verificações e API depende do plano de suporte.
- Ponto de prova e pegadinha: Check recomenda; Health comunica incidente AWS; Compute Optimizer foca dimensionamento.


#### AWS Well-Architected Tool

- O que é: Ferramenta para revisar workloads contra o framework.
- Quando usar: Registrar riscos e melhorias nos seis pilares.
- Quando não usar: Não para escanear continuamente recursos ou aplicar correções.
- Cobrança: Sem taxa adicional da ferramenta.
- Ponto de prova e pegadinha: Framework é orientação; Tool é revisão guiada.


### Migration and Transfer


#### AWS Application Discovery Service

- O que é: Inventário e descoberta de servidores e dependências para migração.
- Quando usar: Entender o ambiente antes de mover workloads; verificar disponibilidade para novos projetos.
- Quando não usar: Não para replicar e lançar servidores migrados: Application Migration Service.
- Cobrança: Sem taxa direta no serviço; armazenamento/análise associados podem custar.
- Ponto de prova e pegadinha: Descobrir o que existe não executa a migração.


#### AWS Application Migration Service

- O que é: Migração de servidores por replicação, conhecida como MGN e também encontrada como AWS Transform MGN.
- Quando usar: Rehost de servidores físicos, virtuais ou em outra nuvem.
- Quando não usar: Não para converter esquema de banco: SCT; nem como estratégia permanente de DR.
- Cobrança: Período inicial elegível por servidor; depois cobrança por tempo, mais infraestrutura durante a replicação.
- Ponto de prova e pegadinha: Replicar, testar e fazer cutover para EC2; não precisa reescrever a aplicação para rehost.


#### AWS Database Migration Service (AWS DMS)

- O que é: Migração e replicação de dados entre fontes e destinos suportados.
- Quando usar: Mover banco com carga inicial e replicação contínua para reduzir indisponibilidade.
- Quando não usar: Não para replicar todos os discos de uma VM ou presumir conversão completa de código SQL.
- Cobrança: Instância/tempo ou capacidade serverless, armazenamento e custos associados.
- Ponto de prova e pegadinha: CDC replica alterações; SCT ou DMS Schema Conversion trata conversão de esquema quando necessária.


#### Migration Evaluator

- O que é: Avaliação de inventário e business case de migração.
- Quando usar: Estimar custo de levar servidores à AWS com base no uso observado.
- Quando não usar: Não para executar a migração nem substituir orçamento de arquitetura detalhado.
- Cobrança: Avaliação oferecida sem custo adicional.
- Ponto de prova e pegadinha: Business case e TCO antes de migrar; comparar com Discovery (inventário) e Hub (acompanhamento).


#### AWS Migration Hub

- O que é: Visão central do andamento de migrações.
- Quando usar: Acompanhar aplicações e progresso de ferramentas integradas; conferir disponibilidade para novos projetos.
- Quando não usar: Não para mover servidor por conta própria.
- Cobrança: Sem taxa adicional para acompanhamento padrão; ferramentas integradas seguem sua cobrança.
- Ponto de prova e pegadinha: Hub acompanha; MGN move servidores; DMS move dados.


#### AWS Schema Conversion Tool (AWS SCT)

- O que é: Ferramenta de avaliação e conversão de esquema entre engines.
- Quando usar: Preparar migração heterogênea, por exemplo Oracle → PostgreSQL, revisando incompatibilidades.
- Quando não usar: Não para assumir que tudo converte sozinho nem substituir replicação contínua.
- Cobrança: Ferramenta sem taxa direta; serviços usados na migração à parte.
- Ponto de prova e pegadinha: Conversão de estrutura e código suportado não equivale a copiar todas as linhas.


### Networking and Content Delivery


#### Amazon API Gateway

- O que é: Entrada gerenciada para publicação de APIs.
- Quando usar: Expor e controlar APIs HTTP, REST ou WebSocket diante de backends.
- Quando não usar: Não para cache global de sites nem balanceamento genérico de TCP.
- Cobrança: Chamadas, tráfego e cache opcional; WebSocket por mensagens e duração de conexão.
- Ponto de prova e pegadinha: API Gateway recebe e encaminha; Lambda executa código; o tipo de API muda as funcionalidades.


#### Amazon CloudFront

- O que é: CDN que distribui conteúdo pela rede de borda.
- Quando usar: Reduzir latência e aplicar cache a conteúdo elegível.
- Quando não usar: Não quando requisito é IP global fixo e aceleração TCP/UDP sem cache: Global Accelerator.
- Cobrança: Transferência, requisições, extras ou planos de preço fixo conforme oferta.
- Ponto de prova e pegadinha: Edge location não é AZ; cache hit evita buscar na origem.


#### AWS Direct Connect

- O que é: Conectividade dedicada entre rede própria e AWS.
- Quando usar: Tráfego híbrido consistente sem depender do caminho da internet pública.
- Quando não usar: Não para começar depressa com túnel barato: Site-to-Site VPN.
- Cobrança: Porta por hora, transferência de saída e possíveis custos de parceiro.
- Ponto de prova e pegadinha: Conexão dedicada não significa criptografia automática; pode ser combinada com VPN.


#### AWS Global Accelerator

- O que é: Aceleração de aplicações TCP/UDP pela rede AWS.
- Quando usar: Usar IPs estáticos anycast e rotear até endpoints saudáveis.
- Quando não usar: Não para fazer cache de imagens ou vídeos: CloudFront.
- Cobrança: Acelerador por hora mais prêmio de transferência.
- Ponto de prova e pegadinha: Acelera o caminho, não armazena conteúdo na borda.


#### AWS PrivateLink

- O que é: Acesso privado a serviços via endpoints de interface.
- Quando usar: Consumir serviço AWS ou de outro provedor sem expor tráfego à internet pública.
- Quando não usar: Não para conectar redes inteiras com roteamento transitivo: Transit Gateway.
- Cobrança: Endpoint por AZ/hora e dados processados, conforme tipo.
- Ponto de prova e pegadinha: Expõe um serviço, não toda a VPC; endpoints gateway de S3/DynamoDB têm modelo distinto.


#### Amazon Route 53

- O que é: DNS gerenciado, registro de domínios e health checks.
- Quando usar: Resolver nomes e direcionar consultas por políticas DNS.
- Quando não usar: Não para balancear requisições HTTP individualmente ou fornecer CDN.
- Cobrança: Zonas, consultas, domínios e checagens; exceções para consultas Alias elegíveis.
- Ponto de prova e pegadinha: DNS indica destino; não é proxy; política de latência e failover é DNS.


#### AWS Transit Gateway

- O que é: Hub de roteamento para VPCs e redes externas.
- Quando usar: Interligar muitas VPCs e conexões híbridas sem malha de peering.
- Quando não usar: Não para publicar um único serviço privado: PrivateLink.
- Cobrança: Anexos por hora e dados processados conforme caminho.
- Ponto de prova e pegadinha: Hub com roteamento transitivo; VPC peering não é transitivo.


#### Amazon VPC

- O que é: Rede virtual isolada regional.
- Quando usar: Separar workloads e controlar sub-redes, rotas e acesso.
- Quando não usar: Não é, por si só, conexão híbrida ou firewall de aplicação.
- Cobrança: VPC básica sem taxa direta; NAT, endpoints, IPv4 público e outros componentes podem custar.
- Ponto de prova e pegadinha: Subnet pertence a uma AZ; SG é stateful e só permite; NACL é stateless e aceita allow/deny.


#### AWS VPN

- O que é: Família de conectividade criptografada.
- Quando usar: Conectar redes ou usuários sem circuito dedicado.
- Quando não usar: Não se o requisito principal é conexão física dedicada: Direct Connect.
- Cobrança: Não tem tarifa única: ver Site-to-Site e Client VPN.
- Ponto de prova e pegadinha: Rede a rede e pessoa a rede são casos distintos.


#### AWS Site-to-Site VPN

- O que é: Túneis IPsec entre redes.
- Quando usar: Conectar escritório/datacenter a VPC ou Transit Gateway.
- Quando não usar: Não para cada colaborador remoto acessar individualmente: Client VPN.
- Cobrança: Conexão por hora e transferência; extras em opções aceleradas.
- Ponto de prova e pegadinha: Normalmente dois túneis por conexão; VPN criptografada não é linha dedicada.


#### AWS Client VPN

- O que é: Acesso remoto gerenciado para dispositivos de usuários.
- Quando usar: Colaboradores acessarem redes privadas via cliente VPN.
- Quando não usar: Não para ligar dois roteadores/sites: Site-to-Site VPN.
- Cobrança: Associações de rede por hora e conexões de clientes por hora.
- Ponto de prova e pegadinha: Autentica usuários; não é navegação isolada do Secure Browser.


### Security, Identity, and Compliance


#### AWS Artifact

- O que é: Portal de relatórios e acordos de conformidade AWS.
- Quando usar: Obter relatórios SOC/ISO e administrar acordos elegíveis.
- Quando não usar: Não para verificar a configuração da sua VPC nem exportar seus logs.
- Cobrança: Sem taxa direta.
- Ponto de prova e pegadinha: A conformidade da AWS não certifica automaticamente sua aplicação.


#### AWS Certificate Manager (ACM)

- O que é: Provisionamento e gestão de certificados TLS.
- Quando usar: Habilitar HTTPS em serviços integrados, como CloudFront e ELB.
- Quando não usar: Não para armazenar senha de banco: Secrets Manager.
- Cobrança: Certificados públicos não exportáveis integrados normalmente sem taxa; exportáveis e CA privada podem ser cobrados.
- Ponto de prova e pegadinha: Certificado TLS protege dados em trânsito; não substitui KMS para chaves de dados.


#### AWS CloudHSM

- O que é: Módulos de segurança de hardware dedicados, com controle do cliente.
- Quando usar: Atender exigência de HSM dedicado e operações criptográficas específicas.
- Quando não usar: Não para criptografia AWS integrada quando KMS atende com menos operação.
- Cobrança: Por HSM-hora.
- Ponto de prova e pegadinha: HSM é cofre físico criptográfico; CloudHSM transfere mais administração ao cliente.


#### Amazon Cognito

- O que é: Identidade para usuários de aplicações web/mobile.
- Quando usar: Cadastro e login de clientes e federação de identidades.
- Quando não usar: Não para dar acesso de colaboradores a várias contas AWS: IAM Identity Center.
- Cobrança: Usuários ativos mensais e recursos conforme plano; SMS pode custar à parte.
- Ponto de prova e pegadinha: User pools autenticam; identity pools podem entregar credenciais AWS temporárias.


#### Amazon Detective

- O que é: Investiga achados de segurança correlacionando dados e relações.
- Quando usar: Entender causa e contexto após um alerta.
- Quando não usar: Não como detector primário de ameaças: GuardDuty.
- Cobrança: Volume de dados ingeridos e fontes conforme uso.
- Ponto de prova e pegadinha: Detective investiga; GuardDuty detecta; Security Hub centraliza achados.


#### AWS Directory Service

- O que é: Serviços de diretório gerenciado e integração com Active Directory.
- Quando usar: Integrar workloads que precisam de AD, como apps Windows.
- Quando não usar: Não como cadastro de consumidores de um aplicativo: Cognito.
- Cobrança: Diretório/controladores por tempo e tipo de oferta.
- Ponto de prova e pegadinha: Managed Microsoft AD hospeda diretório; AD Connector encaminha autenticação ao diretório existente.


#### AWS Firewall Manager

- O que é: Administração centralizada de políticas de segurança de rede.
- Quando usar: Aplicar políticas WAF e outras proteções em várias contas.
- Quando não usar: Não como mecanismo que inspeciona HTTP sozinho: WAF.
- Cobrança: Por política e Região conforme tipo, mais serviços subjacentes; exceções por oferta.
- Ponto de prova e pegadinha: Governa em escala usando Organizations; não confundir com AWS Network Firewall.


#### Amazon GuardDuty

- O que é: Detecção gerenciada de ameaças.
- Quando usar: Identificar atividade suspeita em contas e workloads.
- Quando não usar: Não para inventário de CVEs, certificação ou bloqueio direto de HTTP.
- Cobrança: Volume/eventos analisados e planos de proteção adicionais.
- Ponto de prova e pegadinha: Achado é alerta, não bloqueio; Inspector busca vulnerabilidades.


#### AWS Identity and Access Management (IAM)

- O que é: Controle de autenticação e autorização de recursos AWS.
- Quando usar: Definir acesso mínimo de pessoas, aplicações e serviços.
- Quando não usar: Não para cadastro de usuários finais de um app público: Cognito.
- Cobrança: Recursos básicos sem taxa adicional; recursos especializados podem ter tarifa separada.
- Ponto de prova e pegadinha: Role pode ser assumida com credenciais temporárias; policy autoriza; deny explícito vence allow.


#### AWS IAM Identity Center

- O que é: Acesso centralizado da força de trabalho a contas e aplicações.
- Quando usar: SSO multiaccount com permission sets e IdP integrado.
- Quando não usar: Não para login de consumidores de um app.
- Cobrança: Sem taxa adicional direta; IdP e serviços associados podem custar.
- Ponto de prova e pegadinha: Identity Center gerencia acesso da força de trabalho; IAM roles continuam existindo nas contas.


#### Amazon Inspector

- O que é: Gestão automatizada de vulnerabilidades em workloads suportados.
- Quando usar: Encontrar CVEs e exposições em EC2, imagens ECR e Lambda conforme cobertura.
- Quando não usar: Não para descobrir dados pessoais em buckets: Macie.
- Cobrança: Recursos monitorados e tipo/frequência de escaneamento.
- Ponto de prova e pegadinha: Pista: pacote vulnerável ou imagem de contêiner; GuardDuty procura sinais de ameaça.


#### AWS Key Management Service (AWS KMS)

- O que é: Criação e uso gerenciado de chaves criptográficas.
- Quando usar: Criptografia integrada a S3, EBS, RDS e outros serviços.
- Quando não usar: Não para guardar credenciais, emitir certificados ou exigir HSM dedicado autogerido.
- Cobrança: Chaves gerenciadas pelo cliente e volume de chamadas; regras variam por tipo.
- Ponto de prova e pegadinha: Chave KMS protege chaves de dados; política de chave e permissões importam.


#### Amazon Macie

- O que é: Descoberta de dados sensíveis no S3.
- Quando usar: Identificar dados pessoais ou sigilosos em objetos.
- Quando não usar: Não para detectar CVEs nem descobrir dados em todo banco automaticamente.
- Cobrança: Inventário/avaliação e descoberta por objetos ou bytes conforme modalidade.
- Ponto de prova e pegadinha: Macie foca S3 e dados sensíveis; não é antivírus.


#### AWS Resource Access Manager (AWS RAM)

- O que é: Compartilhamento de recursos AWS suportados entre contas.
- Quando usar: Compartilhar sub-redes ou outros recursos suportados sem duplicação.
- Quando não usar: Não para criar usuários ou aprovar automaticamente qualquer recurso.
- Cobrança: Sem taxa direta do RAM; uso do recurso compartilhado pode custar.
- Ponto de prova e pegadinha: Compartilhar não transfere propriedade nem substitui IAM.


#### AWS Secrets Manager

- O que é: Armazenamento e rotação de segredos de aplicação.
- Quando usar: Rotacionar e recuperar credenciais de banco ou API.
- Quando não usar: Não para armazenar configurações públicas simples ou substituir KMS.
- Cobrança: Segredos armazenados e chamadas de API; recursos usados pela rotação à parte.
- Ponto de prova e pegadinha: Guarda o segredo; KMS fornece criptografia; rotação precisa ser configurada.


#### AWS Security Hub

- O que é: Centralização de achados e avaliações de postura de segurança.
- Quando usar: Consolidar resultados de serviços e conferir controles.
- Quando não usar: Não para inspeção de tráfego ou investigação forense por si só.
- Cobrança: Modelo varia entre Security Hub e Security Hub CSPM e conforme recursos cobertos, verificações e processamento.
- Ponto de prova e pegadinha: Correlacionar achados não substitui GuardDuty, Inspector ou Macie.


#### AWS Shield

- O que é: Proteção contra ataques distribuídos de negação de serviço (DDoS).
- Quando usar: Proteger recursos elegíveis de ataques volumétricos; Advanced para proteções adicionais.
- Quando não usar: Não como substituto de regras HTTP contra padrões maliciosos: WAF.
- Cobrança: Standard incluído; Advanced tem assinatura e possíveis cobranças de uso.
- Ponto de prova e pegadinha: Shield foca DDoS; WAF avalia requisições web; podem atuar juntos.


#### AWS WAF

- O que é: Firewall de aplicação web para inspecionar HTTP(S).
- Quando usar: Bloquear padrões como SQL injection, bots e requisições acima de limites configurados.
- Quando não usar: Não para filtrar todo tráfego TCP/UDP de uma VPC.
- Cobrança: Web ACLs, regras, requisições e recursos opcionais.
- Ponto de prova e pegadinha: WAF é camada 7; SG e NACL trabalham principalmente com endereços, protocolos e portas.


### Serverless


#### AWS Fargate

- O que é: Capacidade serverless para contêineres ECS/EKS.
- Quando usar: Executar contêineres sem gerenciar hosts.
- Quando não usar: Não para exigências de controle do host, GPUs ou configurações não suportadas.
- Cobrança: vCPU, memória e armazenamento adicional por duração.
- Ponto de prova e pegadinha: Fargate é a capacidade, não o orquestrador; não é limitado a funções de 15 minutos.


#### AWS Lambda

- O que é: Execução gerenciada de funções acionadas por eventos.
- Quando usar: Rodar código curto de reação a eventos, APIs e automações.
- Quando não usar: Não para tarefa única acima de 15 minutos ou runtime que precise de host controlado.
- Cobrança: Invocações, GB-segundo e opcionais como concorrência provisionada.
- Ponto de prova e pegadinha: Não administra servidor; precisa gerenciar código, permissões e integrações; estado durável fica fora da função.


### Storage


#### AWS Backup

- O que é: Políticas centralizadas de cópia e restauração de recursos suportados.
- Quando usar: Organizar planos, retenção e cofres para backups.
- Quando não usar: Não para retomar servidores quase imediatamente por replicação contínua: Elastic Disaster Recovery.
- Cobrança: Armazenamento, restauração, cópias e extras conforme recurso e camada.
- Ponto de prova e pegadinha: Backup recupera dados; alta disponibilidade e DR são objetivos diferentes.


#### Amazon Elastic Block Store (Amazon EBS)

- O que é: Volume persistente em blocos para EC2.
- Quando usar: Disco de boot ou de dados com baixa latência.
- Quando não usar: Não para compartilhamento de arquivos entre várias AZs ou objetos web.
- Cobrança: GB provisionados, IOPS/throughput conforme tipo e snapshots.
- Ponto de prova e pegadinha: Volume é zonal; snapshot pode criar novo volume em outra AZ da Região; não confundir com instance store.


#### Amazon Elastic File System (Amazon EFS)

- O que é: Sistema de arquivos elástico NFS.
- Quando usar: Compartilhar arquivos POSIX/Linux entre instâncias e serviços compatíveis.
- Quando não usar: Não para SMB Windows: FSx for Windows File Server; nem para volume de boot típico.
- Cobrança: GB-mês por classe, throughput e acessos conforme configuração.
- Ponto de prova e pegadinha: EFS é arquivo compartilhado, EBS é bloco; EFS Regional e One Zone têm disponibilidades diferentes.


#### AWS Elastic Disaster Recovery

- O que é: Replicação contínua para recuperação de servidores na AWS (DRS).
- Quando usar: Reduzir perda de dados e tempo de recuperação em desastre.
- Quando não usar: Não para arquivamento barato ou simples backup de objetos.
- Cobrança: Por servidor replicado por hora e recursos de staging, teste e recuperação.
- Ponto de prova e pegadinha: RPO é perda de dados tolerável; RTO é tempo tolerável para retomar.


#### Amazon FSx

- O que é: Família gerenciada de sistemas de arquivos especializados.
- Quando usar: Usar Windows File Server/SMB, Lustre para HPC, ONTAP ou OpenZFS conforme necessidade.
- Quando não usar: Não quando um bucket de objetos basta.
- Cobrança: Capacidade, throughput, IOPS e backup conforme engine.
- Ponto de prova e pegadinha: FSx não é um único filesystem; Windows ≠ Lustre.


#### Amazon S3

- O que é: Armazenamento de objetos em buckets.
- Quando usar: Guardar logs, arquivos, data lakes, conteúdo estático e backups.
- Quando não usar: Não para disco de boot de EC2 nem filesystem POSIX genérico.
- Cobrança: GB-mês por classe, operações, recuperação, transferência e extras.
- Ponto de prova e pegadinha: Standard, Intelligent-Tiering, IA, One Zone-IA e classes Glacier; lifecycle transiciona/expira; versionamento preserva versões.


#### Amazon S3 Glacier

- O que é: Classes de arquivamento do S3.
- Quando usar: Guardar histórico de acesso raro de acordo com o prazo de recuperação.
- Quando não usar: Não para dados consultados constantemente e com exigência de acesso imediato sem custo de recuperação.
- Cobrança: Armazenamento, requisições, recuperação e prazo mínimo conforme classe.
- Ponto de prova e pegadinha: Instant Retrieval em milissegundos; Flexible Retrieval em minutos a horas; Deep Archive normalmente horas, não milissegundos.


#### AWS Storage Gateway

- O que é: Integração híbrida de storage local com serviços AWS.
- Quando usar: Acessar armazenamento AWS via interfaces de arquivo, volume ou fita conforme oferta.
- Quando não usar: Não para simples acesso de app cloud ao S3 nem sincronização pontual sem gateway.
- Cobrança: Uso e transferência, operações e armazenamento subjacente conforme modo.
- Ponto de prova e pegadinha: Gateway oferece interface local e pode usar cache; não é sinônimo de migração de banco.


## 3. Analogias e distinções de prova

### VM, imagem, contêiner, ECS, EKS e Fargate

Uma VM é como um apartamento com cozinha própria: tem seu próprio sistema operacional convidado. Um contêiner é como uma estação numa cozinha compartilhada: traz aplicação e dependências, mas compartilha o kernel do host. A imagem do contêiner é a receita embalada, com instruções e ingredientes; o contêiner é uma execução daquela receita. O ECR é o estoque das imagens. ECS e Kubernetes são gerentes de escala: decidem onde cada execução roda e repõem as que falham. EKS é Kubernetes com plano de controle gerenciado pela AWS; Kubernetes agrupa contêineres em pods e os agenda em nós. Fargate fornece a capacidade de execução sem você administrar os hosts. Pegadinha: escolher Fargate não elimina a necessidade de ECS ou EKS; Lambda executa funções, mesmo quando você empacota o código como imagem.

### Rede por camadas: endereço, portaria e recepção

VPC é o condomínio, subnet é uma área dentro de uma AZ e a tabela de rotas indica para qual saída o tráfego vai. Uma subnet pública tem rota ao Internet Gateway, mas isso não basta para expor toda instância: endereçamento, regras e rotas continuam importando. NAT Gateway permite que recursos privados iniciem conexões de saída sem aceitar conexões inesperadas de entrada; seu tempo ativo e dados processados podem ser cobrados. SG é a portaria de cada interface: quando permite a ida, reconhece a volta (stateful). NACL é a cancela da subnet: ida e volta são avaliadas separadamente (stateless), e há regras de permitir e negar. DNS/Route 53 é a agenda de endereços. Um NLB decide pelo transporte (camada 4, como TCP/UDP); um ALB entende HTTP, inclusive caminhos como `/pedidos` (camada 7). WAF inspeciona regras da aplicação. CloudFront coloca cópias elegíveis em filiais próximas; Global Accelerator otimiza o trajeto sem cache. PrivateLink abre acesso a um serviço; Transit Gateway interliga redes.

### Mensageria usando um fluxo antifraude

Imagine uma transação que precisa gerar análise, notificação e auditoria. SQS é a bandeja de trabalho: um consumidor retira a tarefa e confirma o processamento excluindo a mensagem; se não confirmar, ela pode voltar a ficar visível. SNS é o alto-falante: replica a notificação para assinantes. EventBridge é o despachante: examina o conteúdo e encaminha a destinos diferentes. Kinesis é a esteira gravada de eventos: consumidores podem ler novamente dentro da retenção. Step Functions é o fluxograma executável: aplica decisões, espera e repete etapas. Eles podem coexistir. Kafka é uma analogia útil para um stream, mas Amazon MSK está explicitamente fora do escopo publicado.

### Storage, bases e recuperação

S3 é um depósito de objetos etiquetados; EBS é um disco ligado ao servidor; EFS é uma pasta compartilhada NFS; FSx é uma família de pastas e sistemas de arquivos especializados. S3 Standard é para acesso frequente; Intelligent-Tiering ajusta camadas para padrões incertos, com regras de monitoramento e classes opcionais; Standard-IA é menos frequente e multi-AZ; One Zone-IA troca redundância entre AZs por menor custo. Glacier Instant Retrieval mantém acesso em milissegundos; Flexible Retrieval e Deep Archive atendem janelas mais longas. Não confunda durabilidade (reter o dado) com disponibilidade (acessá-lo agora). EBS é persistente, mas pode ser excluído no término da instância se configurado para isso. Backup diário sem outra replicação pode significar até cerca de 24 horas de dados perdidos (RPO); se restaurar leva 3 horas, esse é o tempo de recuperação observado em relação ao RTO. Para um caso de fraude: RDS registra transações, Neptune explora elos entre contas e dispositivos, Redshift agrega tendências, ElastiCache acelera consultas repetidas.

### Auditoria e segurança

CloudTrail é o livro de entrada: quem fez o quê. Config é o álbum de estados e a régua de conformidade. CloudWatch é o painel de instrumentos. GuardDuty é o alarme de comportamento suspeito; Inspector confere vulnerabilidades conhecidas; Macie procura documentos sensíveis no S3; Detective investiga o contexto; Security Hub reúne achados e controles. Artifact dá evidências sobre a AWS, não sobre a sua configuração. KMS controla a chave criptográfica; Secrets Manager guarda e pode rotacionar a senha; ACM administra o certificado que ajuda a proteger o tráfego TLS.

## 4. Recursos citados pelo programa que não são linhas independentes do catálogo

- Elastic Load Balancing: distribui tráfego a destinos saudáveis. ALB para HTTP(S) e roteamento por host/caminho; NLB para transporte e requisitos como TCP/UDP. Em geral cobra tempo e unidades de capacidade; escolha Auto Scaling para mudar quantidade de destinos.
- Amazon EC2 instance store: armazenamento local temporário, incluído nos tipos suportados; para persistência use EBS ou outro armazenamento durável. Reboot não equivale a stop/terminate.
- AWS Pricing Calculator: estimativa antes da implantação, não é fatura real nem substitui monitoramento. AWS Support Center, Health API, re:Post, Knowledge Center, Prescriptive Guidance, APN e AWS SDKs são referências ou interfaces do programa, não linhas adicionais do catálogo oficial. AWS Bedrock não aparece na lista de entradas em escopo consultada; não presuma exclusão categórica só por ausência numa lista não exaustiva.


## 5. Links oficiais para importar no NotebookLM


### Guia, fundamentos e recursos complementares


- [Guia oficial em português (PDF)](https://docs.aws.amazon.com/pt_br/aws-certification/latest/cloud-practitioner-02/cloud-practitioner-02.pdf)
- [Guia oficial online](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/cloud-practitioner-02.html)
- [Serviços em escopo](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/clf-02-in-scope-services.html)
- [Serviços fora do escopo](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/clf-02-out-of-scope-services.html)
- [Tecnologias e conceitos](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/clf-technologies-concepts.html)
- [Domínio 1](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/cloud-practitioner-02-domain1.html)
- [Domínio 2](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/cloud-practitioner-02-domain2.html)
- [Domínio 3](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/cloud-practitioner-02-domain3.html)
- [Domínio 4](https://docs.aws.amazon.com/aws-certification/latest/cloud-practitioner-02/cloud-practitioner-02-domain4.html)
- [Visão geral dos serviços AWS](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/introduction.html)
- [Preços AWS](https://aws.amazon.com/pricing/)
- [AWS Pricing Calculator](https://calculator.aws/)
- [Planos AWS Support](https://docs.aws.amazon.com/awssupport/latest/user/aws-support-plans.html)
- [Transição dos planos de suporte](https://docs.aws.amazon.com/awssupport/latest/user/support-plans-eos.html)
- [Comparação e preços dos planos](https://aws.amazon.com/premiumsupport/plans/)
- [Responsabilidade compartilhada](https://aws.amazon.com/compliance/shared-responsibility-model/)
- [Tarefas que requerem root](https://docs.aws.amazon.com/IAM/latest/UserGuide/root-user-tasks.html)
- [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html)
- [AWS CAF](https://aws.amazon.com/cloud-adoption-framework/)
- [Estratégias de migração](https://docs.aws.amazon.com/prescriptive-guidance/latest/large-migration-guide/migration-strategies.html)
- [Infraestrutura global](https://aws.amazon.com/about-aws/global-infrastructure/)
- [Opções de compra EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-purchasing-options.html)
- [Elastic Load Balancing](https://aws.amazon.com/elasticloadbalancing/pricing/)
- [Instance store](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html)
- [Classes de armazenamento S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html)
- [AWS Security Center](https://aws.amazon.com/security/)
- [AWS Security Blog](https://aws.amazon.com/blogs/security/)
- [AWS Knowledge Center](https://repost.aws/knowledge-center)
- [AWS re:Post](https://repost.aws/)
- [AWS Prescriptive Guidance](https://aws.amazon.com/prescriptive-guidance/)
- [AWS Partner Network](https://aws.amazon.com/partners/)
- [AWS SDKs](https://aws.amazon.com/developer/tools/)
- [AWS Support Center](https://console.aws.amazon.com/support/home)
- [Denunciar abuso](https://aws.amazon.com/forms/report-abuse)
- [AWS Professional Services](https://aws.amazon.com/professional-services/)
- [AWS Health API](https://docs.aws.amazon.com/health/latest/ug/health-api.html)
- [AWS Data Exports](https://docs.aws.amazon.com/cur/latest/userguide/what-is-data-exports.html)

### Analytics — páginas oficiais dos serviços
- [Amazon Athena](https://aws.amazon.com/athena/pricing/)
- [Amazon EMR](https://aws.amazon.com/emr/pricing/)
- [AWS Glue](https://aws.amazon.com/glue/pricing/)
- [Amazon Kinesis](https://aws.amazon.com/kinesis/data-streams/pricing/)
- [Amazon OpenSearch Service](https://aws.amazon.com/opensearch-service/pricing/)
- [Amazon Quick](https://aws.amazon.com/quick/pricing/)
- [Amazon Redshift](https://aws.amazon.com/redshift/pricing/)

### Application Integration — páginas oficiais dos serviços
- [Amazon EventBridge](https://aws.amazon.com/eventbridge/pricing/)
- [Amazon Simple Notification Service (Amazon SNS)](https://aws.amazon.com/sns/pricing/)
- [Amazon Simple Queue Service (Amazon SQS)](https://aws.amazon.com/sqs/pricing/)
- [AWS Step Functions](https://aws.amazon.com/step-functions/pricing/)

### Business Applications — páginas oficiais dos serviços
- [Amazon Connect](https://aws.amazon.com/connect/pricing/)
- [Amazon Simple Email Service (Amazon SES)](https://aws.amazon.com/ses/pricing/)

### Cloud Financial Management — páginas oficiais dos serviços
- [AWS Budgets](https://aws.amazon.com/aws-cost-management/aws-budgets/pricing/)
- [AWS Cost and Usage Reports](https://aws.amazon.com/aws-cost-management/aws-cost-and-usage-reporting/pricing/)
- [AWS Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/pricing/)
- [AWS Marketplace](https://aws.amazon.com/marketplace/pricing/)

### Compute — páginas oficiais dos serviços
- [AWS Batch](https://aws.amazon.com/batch/pricing/)
- [Amazon EC2](https://aws.amazon.com/ec2/pricing/)
- [AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/pricing/)
- [Amazon Lightsail](https://aws.amazon.com/lightsail/pricing/)
- [AWS Outposts](https://aws.amazon.com/outposts/pricing/)

### Containers — páginas oficiais dos serviços
- [Amazon Elastic Container Registry (Amazon ECR)](https://aws.amazon.com/ecr/pricing/)
- [Amazon Elastic Container Service (Amazon ECS)](https://aws.amazon.com/ecs/pricing/)
- [Amazon Elastic Kubernetes Service (Amazon EKS)](https://aws.amazon.com/eks/pricing/)

### Customer Enablement — páginas oficiais dos serviços
- [AWS Support](https://aws.amazon.com/premiumsupport/pricing/)

### Database — páginas oficiais dos serviços
- [Amazon Aurora](https://aws.amazon.com/rds/aurora/pricing/)
- [Amazon DocumentDB](https://aws.amazon.com/documentdb/pricing/)
- [Amazon DynamoDB](https://aws.amazon.com/dynamodb/pricing/)
- [Amazon ElastiCache](https://aws.amazon.com/elasticache/pricing/)
- [Amazon Neptune](https://aws.amazon.com/neptune/pricing/)
- [Amazon RDS](https://aws.amazon.com/rds/pricing/)

### Developer Tools — páginas oficiais dos serviços
- [AWS CLI](https://aws.amazon.com/cli/)
- [AWS CodeBuild](https://aws.amazon.com/codebuild/pricing/)
- [AWS CodePipeline](https://aws.amazon.com/codepipeline/pricing/)
- [AWS X-Ray](https://aws.amazon.com/xray/pricing/)

### End User Computing — páginas oficiais dos serviços
- [Amazon AppStream 2.0](https://aws.amazon.com/appstream2/pricing/)
- [Amazon WorkSpaces](https://aws.amazon.com/workspaces/pricing/)
- [Amazon WorkSpaces Secure Browser](https://aws.amazon.com/workspaces/secure-browser/pricing/)

### Frontend Web and Mobile — páginas oficiais dos serviços
- [AWS Amplify](https://aws.amazon.com/amplify/pricing/)

### Internet of Things (IoT) — páginas oficiais dos serviços
- [AWS IoT Core](https://aws.amazon.com/iot-core/pricing/)

### Machine Learning — páginas oficiais dos serviços
- [Amazon Comprehend](https://aws.amazon.com/comprehend/pricing/)
- [Amazon Lex](https://aws.amazon.com/lex/pricing/)
- [Amazon Polly](https://aws.amazon.com/polly/pricing/)
- [Amazon Q](https://aws.amazon.com/amazon-q/pricing/)
- [Amazon Rekognition](https://aws.amazon.com/rekognition/pricing/)
- [Amazon SageMaker AI](https://aws.amazon.com/sagemaker-ai/pricing/)
- [Amazon Textract](https://aws.amazon.com/textract/pricing/)
- [Amazon Transcribe](https://aws.amazon.com/transcribe/pricing/)
- [Amazon Translate](https://aws.amazon.com/translate/pricing/)

### Management and Governance — páginas oficiais dos serviços
- [AWS Auto Scaling](https://aws.amazon.com/autoscaling/pricing/)
- [AWS CloudFormation](https://aws.amazon.com/cloudformation/pricing/)
- [AWS CloudTrail](https://aws.amazon.com/cloudtrail/pricing/)
- [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/pricing/)
- [AWS Compute Optimizer](https://aws.amazon.com/compute-optimizer/pricing/)
- [AWS Config](https://aws.amazon.com/config/pricing/)
- [AWS Control Tower](https://aws.amazon.com/controltower/pricing/)
- [AWS Health Dashboard](https://health.aws.amazon.com/health/status)
- [AWS License Manager](https://aws.amazon.com/license-manager/pricing/)
- [AWS Management Console](https://aws.amazon.com/console/)
- [AWS Organizations](https://aws.amazon.com/organizations/pricing/)
- [AWS Service Catalog](https://aws.amazon.com/servicecatalog/pricing/)
- [Service Quotas](https://aws.amazon.com/servicequotas/)
- [AWS Systems Manager](https://aws.amazon.com/systems-manager/pricing/)
- [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/)
- [AWS Well-Architected Tool](https://aws.amazon.com/well-architected-tool/pricing/)

### Migration and Transfer — páginas oficiais dos serviços
- [AWS Application Discovery Service](https://docs.aws.amazon.com/application-discovery/latest/userguide/what-is-appdiscovery.html)
- [AWS Application Migration Service](https://aws.amazon.com/application-migration-service/pricing/)
- [AWS Database Migration Service (AWS DMS)](https://aws.amazon.com/dms/pricing/)
- [Migration Evaluator](https://aws.amazon.com/migration-evaluator/)
- [AWS Migration Hub](https://aws.amazon.com/migration-hub/pricing/)
- [AWS Schema Conversion Tool (AWS SCT)](https://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_Welcome.html)

### Networking and Content Delivery — páginas oficiais dos serviços
- [Amazon API Gateway](https://aws.amazon.com/api-gateway/pricing/)
- [Amazon CloudFront](https://aws.amazon.com/cloudfront/pricing/)
- [AWS Direct Connect](https://aws.amazon.com/directconnect/pricing/)
- [AWS Global Accelerator](https://aws.amazon.com/global-accelerator/pricing/)
- [AWS PrivateLink](https://aws.amazon.com/privatelink/pricing/)
- [Amazon Route 53](https://aws.amazon.com/route53/pricing/)
- [AWS Transit Gateway](https://aws.amazon.com/transit-gateway/pricing/)
- [Amazon VPC](https://aws.amazon.com/vpc/pricing/)
- [AWS VPN](https://aws.amazon.com/vpn/pricing/)
- [AWS Site-to-Site VPN](https://aws.amazon.com/vpn/pricing/)
- [AWS Client VPN](https://aws.amazon.com/vpn/pricing/)

### Security, Identity, and Compliance — páginas oficiais dos serviços
- [AWS Artifact](https://aws.amazon.com/artifact/pricing/)
- [AWS Certificate Manager (ACM)](https://aws.amazon.com/certificate-manager/pricing/)
- [AWS CloudHSM](https://aws.amazon.com/cloudhsm/pricing/)
- [Amazon Cognito](https://aws.amazon.com/cognito/pricing/)
- [Amazon Detective](https://aws.amazon.com/detective/pricing/)
- [AWS Directory Service](https://aws.amazon.com/directoryservice/pricing/)
- [AWS Firewall Manager](https://aws.amazon.com/firewall-manager/pricing/)
- [Amazon GuardDuty](https://aws.amazon.com/guardduty/pricing/)
- [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/pricing/)
- [AWS IAM Identity Center](https://aws.amazon.com/iam/identity-center/pricing/)
- [Amazon Inspector](https://aws.amazon.com/inspector/pricing/)
- [AWS Key Management Service (AWS KMS)](https://aws.amazon.com/kms/pricing/)
- [Amazon Macie](https://aws.amazon.com/macie/pricing/)
- [AWS Resource Access Manager (AWS RAM)](https://aws.amazon.com/ram/pricing/)
- [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/pricing/)
- [AWS Security Hub](https://aws.amazon.com/security-hub/pricing/)
- [AWS Shield](https://aws.amazon.com/shield/pricing/)
- [AWS WAF](https://aws.amazon.com/waf/pricing/)

### Serverless — páginas oficiais dos serviços
- [AWS Fargate](https://aws.amazon.com/fargate/pricing/)
- [AWS Lambda](https://aws.amazon.com/lambda/pricing/)

### Storage — páginas oficiais dos serviços
- [AWS Backup](https://aws.amazon.com/backup/pricing/)
- [Amazon Elastic Block Store (Amazon EBS)](https://aws.amazon.com/ebs/pricing/)
- [Amazon Elastic File System (Amazon EFS)](https://aws.amazon.com/efs/pricing/)
- [AWS Elastic Disaster Recovery](https://aws.amazon.com/disaster-recovery/pricing/)
- [Amazon FSx](https://aws.amazon.com/fsx/pricing/)
- [Amazon S3](https://aws.amazon.com/s3/pricing/)
- [Amazon S3 Glacier](https://aws.amazon.com/s3/pricing/)
- [AWS Storage Gateway](https://aws.amazon.com/storagegateway/pricing/)
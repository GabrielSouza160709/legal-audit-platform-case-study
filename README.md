# Plataforma de Auditoria Patrimonial e Jurídica

Plataforma web em desenvolvimento para apoiar a organização de auditorias patrimoniais, jurídicas e documentais. O produto busca reduzir a fragmentação entre consultas, documentos, entidades relacionadas, evidências e relatórios, mantendo a revisão humana como parte central do processo. O código-fonte é privado.

> Este projeto está em desenvolvimento. O código-fonte, os documentos processados e os dados internos permanecem privados por confidencialidade, segurança e propriedade intelectual. Este repositório apresenta somente um estudo de caso técnico do produto.

## Visão geral

Auditorias patrimoniais e jurídicas dependem de fontes com coberturas, formatos, regras de acesso e níveis de autoridade diferentes. Quando dados estruturados, certidões, bases públicas e retornos de fornecedores ficam dispersos, aumenta o trabalho manual para acompanhar consultas, relacionar entidades, revisar divergências e preparar relatórios.

A plataforma centraliza o ciclo da auditoria em um dossiê digital. Ela organiza entidades, requisições externas, documentos, evidências, achados e decisões humanas, preservando a origem e as limitações de cada informação. Rastreabilidade é um requisito do produto: uma interpretação deve poder ser confrontada com o material que a sustenta.

## Problema abordado

- Consultas distribuídas entre fontes públicas, comerciais e de acesso restrito.
- Documentos em formatos e níveis de confiabilidade distintos.
- Necessidade de relacionar pessoas, empresas, bens e ocorrências sem perder o contexto.
- Dificuldade para acompanhar progresso, pendências, custos e falhas de uma auditoria.
- Produção manual de relatórios a partir de evidências dispersas.
- Dependência de serviços externos sujeitos a indisponibilidade, mudanças e cobertura parcial.

O sistema não pretende eliminar integralmente o trabalho manual. Seu papel é estruturar o processo e tornar a revisão mais consistente e auditável.

## Objetivos do produto

- Centralizar auditorias e entidades relacionadas.
- Organizar documentos, consultas e evidências com rastreabilidade.
- Automatizar consultas quando houver viabilidade técnica, autorização e cobertura adequada.
- Normalizar retornos externos sem apagar sua origem ou suas limitações.
- Identificar achados, incongruências e tarefas que exigem revisão.
- Consolidar informações em relatórios versionados.
- Usar inteligência artificial como apoio à síntese e à análise.
- Manter decisões relevantes sob responsabilidade humana.

## Estado atual

### Implementado

- Autenticação centralizada, sessões web, autorização por papéis e isolamento organizacional.
- Criação, listagem, arquivamento e acompanhamento de auditorias.
- Cadastro de entidades, relacionamentos, tarefas investigativas, hipóteses, incongruências e decisões humanas.
- Dossiê com progresso, cobertura de fontes, achados, evidências e grafo de relações.
- Upload validado de PDFs, armazenamento privado, processamento por páginas, classificação, revisão, vínculos com entidades e redação de áreas sensíveis.
- Fluxo de auditoria exclusivamente documental, sem disparar consultas externas.
- Registro de relatórios, modelos, rascunhos, versões e geração de PDF com vínculo às evidências selecionadas.
- Histórico de eventos e registros de execução para apoiar rastreabilidade operacional.

### Em desenvolvimento ou validação

- Conectores externos reais, que permanecem condicionados a configuração, credenciais, custo, cobertura e validação com evidência permitida.
- Orquestração assíncrona com Redis e Taskiq, disponível por configuração e ainda em processo de estabilização operacional.
- Relatórios documentais em múltiplos volumes e importação organizada de acervos extensos.
- Assistente de IA contextual, com conversas, referências a evidências e revisão humana obrigatória.
- Processamento de documentos heterogêneos e validação com volumes maiores.
- Ampliação de controles de segurança, testes de carga, observabilidade e validação jurídica dos fluxos.

### Planejado

- Expandir conectores de forma incremental, priorizando fontes gratuitas e oficiais quando forem adequadas.
- Evoluir a busca e a correlação de conteúdo documental, inclusive com recursos semânticos.
- Ampliar métricas de tempo, custo, cobertura e pendências.
- Avançar o módulo de análise de imóveis rurais somente após os gates técnicos e de fonte documentados.
- Validar os fluxos com usuários e cenários reais devidamente autorizados e anonimizados.

## Funcionalidades principais

**Gestão de auditorias e dossiês.** Reúne o objeto da análise, as entidades relacionadas, o estágio da investigação, pendências e decisões em uma visão única.

**Documentos e evidências.** Recebe PDFs com validações de arquivo, mantém versões, processa conteúdo por página e permite classificar, revisar, vincular e redigir material sensível.

**Investigação assistida.** Organiza hipóteses, incongruências, tarefas e achados, registrando decisões humanas.

**Relações e cobertura.** Apresenta conexões entre entidades em grafo e informa quais fontes foram consultadas, estão indisponíveis ou ainda precisam de ação manual.

**Relatórios.** Permite montar rascunhos, selecionar evidências e produzir versões em PDF. A composição multi-volume está em validação.

**Assistente contextual.** Apoia a leitura do dossiê, a organização de informações e a explicação de achados, sempre limitado ao contexto disponível e sem autonomia para concluir questões jurídicas.

## Fontes e integrações

- **PGFN:** consulta local sobre dados abertos oficiais previamente importados. O retorno é estruturado e sua atualidade depende da versão da base carregada; ausência de registro não é conclusão automática.
- **Brasil API:** adaptador para dados cadastrais empresariais e quadro societário. É um agregador público e não substitui certidão oficial.
- **InfoSimples:** integração comercial para diferentes consultas, certidões, processos e comprovantes. É paga, exige credencial e consentimento operacional explícito, e permanece desabilitada por padrão.
- **Fontes públicas oficiais:** existem adaptadores e contratos para bases de controle, sanções, processos e compras públicas. A disponibilidade varia entre integrado, preparado mas desabilitado e dependente de credencial.
- **Identidade e arquivos:** Keycloak é utilizado na autenticação e MinIO no armazenamento privado de documentos.
- **Inteligência artificial:** um provedor configurável apoia conversas e análises. Configurações internas e prompts não são publicados.

A plataforma diferencia documento oficial emitido pelo órgão, documento convertido ou renderizado, relatório de fornecedor e dado estruturado em JSON, XML ou formato semelhante. Dado estruturado facilita busca e correlação, mas não substitui automaticamente uma certidão ou documento oficial. Nem todas as fontes fornecem documentos oficiais.

## Tecnologias utilizadas

### Backend

Python 3.12, FastAPI, Pydantic, SQLAlchemy assíncrono, Alembic, Docling, pypdf e WeasyPrint.

### Frontend

Next.js 15, React 19, TypeScript, Tailwind CSS, shadcn/ui, React Flow e Dagre.

### Dados e tarefas assíncronas

PostgreSQL com pgvector, Redis e Taskiq.

### Autenticação e segurança

Keycloak, NextAuth, OIDC, tokens JWT, autorização por papéis e limitação de requisições.

### Arquivos e infraestrutura

MinIO, Docker, Docker Compose e pipelines de integração contínua.

### Inteligência artificial

A IA é uma camada de apoio para síntese, explicação, organização e análise contextual. Provedores, prompts e parâmetros internos permanecem privados.

## Arquitetura conceitual

1. O usuário autenticado cria ou acessa uma auditoria.
2. Entidades e documentos são associados ao dossiê.
3. Consultas autorizadas podem ser encaminhadas ao processamento assíncrono.
4. Adaptadores consultam fontes compatíveis com a política e o escopo.
5. Retornos são normalizados sem perder origem, data, autoridade e limitações.
6. Documentos e evidências são armazenados de forma controlada.
7. Achados, hipóteses e incongruências são apresentados para revisão.
8. Evidências aprovadas podem compor relatórios versionados.
9. A IA auxilia na síntese e na análise, sem substituir a decisão profissional.

## Decisões técnicas relevantes

**Processamento assíncrono.** Consultas externas e processamento documental podem ser lentos ou falhar. Filas e workers evitam bloquear a interação principal e permitem acompanhar tentativas e estados.

**Rastreabilidade das fontes.** Cada execução deve preservar origem, momento, cobertura, custo conhecido, versão de processamento e limitações relevantes.

**Separação entre evidência e interpretação.** Resumos, classificações e achados são camadas derivadas. O material original continua sendo a referência para revisão.

**Dependências externas não confiáveis.** APIs podem mudar formato, limitar acesso ou ficar indisponíveis. Integrações usam políticas explícitas, limites e estados que não confundem falha com ausência de resultado.

**IA com revisão humana.** Conteúdo gerado pode conter erros e deve ser associado às evidências disponíveis. Conclusões formais permanecem humanas.

**Isolamento e modularidade.** Auditorias são separadas por contexto organizacional e os adaptadores de fontes são desacoplados do domínio principal, facilitando evolução controlada.

## Segurança e privacidade

O projeto inclui autenticação, autorização, isolamento organizacional, validação de entradas, controle de CORS, headers de segurança, limitação de requisições, armazenamento privado, proteção de segredos por configuração externa e validações específicas para uploads. Há também recursos de redação e trilhas de eventos.

Esses controles não representam promessa de segurança absoluta nem declaração de conformidade completa com a LGPD. Testes de segurança, carga, operação e revisão jurídica continuam evoluindo. Dados pessoais e documentos sensíveis exigem finalidade, base legal, acesso mínimo e procedimentos adequados ao contexto de uso.

## Inteligência artificial

A IA apoia resumos, organização de informações, chat contextual e elaboração assistida de relatórios. Ela não substitui análise jurídica, não valida sozinha documentos e não deve produzir conclusões autônomas. Respostas podem conter erros e exigem confronto com as evidências e revisão humana. Dados sensíveis não devem ser enviados a provedores externos sem controles apropriados.

## Limitações atuais

- Dependência de APIs, bases e órgãos externos, com cobertura e disponibilidade variáveis.
- Fontes que exigem credenciais, pagamento, CAPTCHA, certificado ou operação manual.
- Diferenças entre jurisdições e formatos documentais.
- Bases locais cuja atualidade depende de importações periódicas.
- Conectores e módulos ainda desabilitados ou em validação.
- Necessidade de revisão humana para evidências, achados e conteúdo gerado por IA.
- Validação de escala, observabilidade e cobertura de testes ainda em expansão.

## Próximas etapas

- Concluir a validação dos conectores prioritários com evidência autorizada.
- Ampliar testes automatizados e cenários de volume.
- Reforçar observabilidade, segurança e controle de custos.
- Estabilizar relatórios multi-volume e fluxos documentais extensos.
- Evoluir a experiência de revisão e a rastreabilidade das conclusões.

## Minha participação

Atuo no levantamento do problema, definição do produto, desenho da arquitetura e desenvolvimento das camadas backend e frontend. Minha participação também abrange modelagem de dados, integrações, processamento assíncrono, documentos e relatórios, aplicação responsável de IA, infraestrutura local, análise de custo de fontes, documentação e validação técnica dos fluxos. O trabalho é conduzido de forma incremental, com separação entre funcionalidades comprovadas, itens em validação e hipóteses futuras.

## Status do projeto

**Em desenvolvimento.** A arquitetura principal está implementada em ambiente de desenvolvimento, enquanto conectores, relatórios multi-volume e módulos especializados seguem em integração e validação.

## Confidencialidade

O código-fonte permanece privado, e dados ou documentos reais não são disponibilizados. Este repositório contém somente documentação de alto nível. Futuras imagens serão publicadas apenas após anonimização e revisão. Detalhes sensíveis da arquitetura, configurações e propriedade intelectual não serão expostos. O objetivo é demonstrar experiência técnica sem divulgar informações jurídicas, comerciais ou pessoais.

## Contato

Gabriel Souza

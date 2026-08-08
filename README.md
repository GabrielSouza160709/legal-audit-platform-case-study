# Plataforma de Auditoria Patrimonial e Jurídica

> Estudo de caso técnico. O código-fonte, os documentos processados e os dados internos permanecem privados por confidencialidade, segurança e propriedade intelectual.

**O problema:** auditorias patrimoniais e jurídicas dependem de fontes com formatos, coberturas e níveis de autoridade diferentes. Quando certidões, bases públicas e retornos de fornecedores ficam dispersos, cresce o trabalho manual de acompanhar consultas, relacionar entidades e montar relatórios.

**A solução:** uma plataforma web que centraliza o ciclo da auditoria em um dossiê digital, organizando entidades, documentos, evidências, achados e decisões humanas — preservando origem e limitações de cada informação.

**Stack:** Python 3.12 · FastAPI · SQLAlchemy · PostgreSQL/pgvector · Redis · Taskiq · Keycloak · MinIO · Next.js 15 · React 19 · TypeScript · Docker

**Escala:** mais de 40 documentos processados por auditoria.

**Status:** em desenvolvimento ativo. Arquitetura principal implementada; conectores externos e relatórios multi-volume em validação.

---

## Tecnologias

**Backend** — Python 3.12, FastAPI, Pydantic, SQLAlchemy assíncrono, Alembic, Docling, pypdf, WeasyPrint
**Frontend** — Next.js 15, React 19, TypeScript, Tailwind CSS, shadcn/ui, React Flow, Dagre
**Dados e filas** — PostgreSQL com pgvector, Redis, Taskiq
**Segurança** — Keycloak, NextAuth, OIDC, JWT, autorização por papéis, rate limiting
**Infraestrutura** — MinIO, Docker, Docker Compose, CI

---

## O que está implementado

- **Dossiê digital** — reúne objeto da análise, entidades relacionadas, estágio da investigação, pendências e decisões em uma visão única, com grafo de relações
- **Pipeline de documentos** — upload validado de PDFs, armazenamento privado, processamento por página, classificação, revisão, vínculo a entidades e redação de áreas sensíveis
- **Investigação assistida** — hipóteses, incongruências, tarefas e achados, com registro das decisões humanas
- **Relatórios versionados** — rascunhos, modelos, seleção de evidências e geração de PDF com vínculo direto ao material que sustenta cada conclusão
- **Controle de acesso** — autenticação centralizada, sessões web, autorização por papéis e isolamento organizacional entre clientes
- **Rastreabilidade operacional** — histórico de eventos e registros de execução

## Em validação

- Conectores externos reais, condicionados a credenciais, custo, cobertura e validação com evidência autorizada
- Orquestração assíncrona com Redis e Taskiq — disponível por configuração, em estabilização operacional
- Relatórios documentais multi-volume e importação de acervos extensos
- Assistente de IA contextual com referências a evidências e revisão humana obrigatória

---

## Arquitetura

1. Usuário autenticado cria ou acessa uma auditoria
2. Entidades e documentos são associados ao dossiê
3. Consultas autorizadas vão para processamento assíncrono
4. Adaptadores consultam fontes compatíveis com a política e o escopo
5. Retornos são normalizados sem perder origem, data, autoridade e limitações
6. Achados, hipóteses e incongruências são apresentados para revisão humana
7. Evidências aprovadas compõem relatórios versionados

### Decisões técnicas

**Processamento assíncrono.** Consultas externas e processamento documental são lentos e falham. Filas e workers evitam bloquear a interação principal e permitem acompanhar tentativas e estados.

**Separação entre evidência e interpretação.** Resumos, classificações e achados são camadas derivadas. O material original continua sendo a referência para revisão.

**Dependências externas não confiáveis.** APIs mudam de formato, limitam acesso e ficam indisponíveis. As integrações usam políticas explícitas e estados que não confundem falha com ausência de resultado.

**IA com revisão humana obrigatória.** A IA apoia síntese, organização e explicação de achados. Conclusões jurídicas permanecem humanas.

---

## Fontes e integrações

| Fonte | Tipo | Situação |
|---|---|---|
| PGFN | Dados abertos oficiais, consulta local | Integrado |
| Brasil API | Cadastro empresarial e quadro societário | Integrado |
| InfoSimples | Certidões, processos e comprovantes (pago) | Desabilitado por padrão |
| Bases públicas de sanções e compras | Adaptadores e contratos | Variável |

A plataforma distingue documento oficial, documento convertido, relatório de fornecedor e dado estruturado. Dado estruturado facilita busca e correlação, mas não substitui certidão oficial. Ausência de registro não é conclusão automática.

---

## Segurança e privacidade

Autenticação, autorização por papéis, isolamento organizacional, validação de entradas, CORS, headers de segurança, rate limiting, armazenamento privado, segredos por configuração externa, validações de upload, redação de conteúdo sensível e trilhas de eventos.

Esses controles não representam garantia de segurança absoluta nem conformidade integral com a LGPD. Dados pessoais e documentos sensíveis exigem finalidade, base legal, acesso mínimo e procedimentos adequados ao contexto de uso.

---

## Minha participação

Levantamento do problema, definição do produto, arquitetura da solução e especificação técnica de todas as camadas. Conduzi a implementação orquestrando agentes de código: escrevi as specs com escopo, critérios de aceite e dependências, e fiz a validação e revisão de cada entrega.

Também atuei na modelagem de dados, no desenho das integrações e do processamento assíncrono, na definição do fluxo documental e de relatórios, na aplicação responsável de IA, na análise de custo das fontes e na validação técnica dos fluxos. O trabalho é conduzido de forma incremental, com separação entre funcionalidades comprovadas, itens em validação e hipóteses futuras.

---

**Gabriel Souza** — [LinkedIn](https://www.linkedin.com/in/gabrielbsouza16/) · [GitHub](https://github.com/GabrielSouza160709)

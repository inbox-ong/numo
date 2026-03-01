# Contribuindo para o Numo (Contributing to Numo)

Bem-vindo à comunidade Numo! Estamos entusiasmados com o seu interesse em contribuir para o futuro da Infraestrutura Pública Digital (DPI) e sistemas financeiros soberanos de código aberto.

Para estruturar e escalar nosso impacto globalmente, a comunidade Numo opera baseada em **Papéis de Colaboração (Roles)** definidos e um fluxo de governança **RFC (Request for Comments)**.

## 👥 Papéis na Comunidade (Community Roles)

Nós acreditamos que um sistema de liquidação soberano não é construído apenas com código, mas com profunda expertise de negócios e testes rigorosos. Encontre o perfil que melhor se adapta às suas habilidades:

### 1. Especialistas (Domain Experts / Business Analysts)
*Perfil*: Profissionais do mercado financeiro, Reguladores, Juristas e Especialistas em Pagamentos.
* **O que fazem**: Escrevem as regras de negócio, definem o comportamento de liquidação e garantem a aderência às normas (ex: manuais do Banco Central, adequações ISO 20022).
* **Como colaboram**: 
  - Levantam demandas abrindo *Issues* com o rótulo `Feature Request`.
  - Escrevem e validam diagramas de fluxo de compensação.
  - Participam das reuniões públicas de "Priorização de Backlog".
  - Analisam as propostas arquiteturais (RFCs) sob a ótica de negócios.

### 2. Desenvolvedores (Core Tech & Integrators)
*Perfil*: Engenheiros de Software (Go, Rust, TypeScript), Arquitetos de Soluções e Engenheiros de Produção (DevOps/SRE).
* **O que fazem**: Traduzem as regras governamentais em código, melhoram a performance do motor de mensageria RTGS, refinam a tolerância a falhas do ledger e constroem SDKs de integração.
* **Como colaboram**:
  - Buscam *Issues* aprovadas e prontas para o desenvolvimento (rótulo `Ready for Dev`).
  - Submetem PRs (*Pull Requests*) contendo a implementação.
  - Prestam suporte técnico em *Code Reviews* de outros desenvolvedores.

### 3. Testers / Auditores (QA & Security)
*Perfil*: Engenheiros de Qualidade (QA), Auditores de Segurança da Informação, Criptógrafos e Hackers Éticos.
* **O que fazem**: Levam o sistema ao limite, garantindo a solidez institucional da infraestrutura. Defendem a rede contra ataques estatais ou vulnerabilidades sistêmicas.
* **Como colaboram**:
  - Estressam o "Nó Raiz" construindo relatórios de liquidações massivas sob alta latência.
  - Auditam contratos inteligentes e transações atômicas contra vulnerabilidades de dupla-gasto (*double-spending*).
  - Penetram as camadas de Defesa e validam a criptografia ponta a ponta (mTLS 1.3, HSM).
  - Suas validações são obrigatórias antes da mudança de *Release Candidate* (RC) para Versão Estável.

---

## 🔄 O Fluxo Numo: Da Ideação ao Código Público

Para manter a ordem e a segurança máxima, todas as alterações significativas passam pelas seguintes etapas:

### 1. Ideação (Levantamento do Problema)
Tudo começa com uma Issue no GitHub. Um **Especialista** identifica uma lacuna na regra de negócio ou um **Tester** reporta um gargalo sistêmico. Se a comunidade julgar pertinente, a Issue entra no backlog.

### 2. Design Document (RFC - Request for Comments)
Antes de escrever código para novas features complexas (ex: "Suporte a Crédito Transfronteiriço"), criamos um documento chamado **RFC** na pasta `/docs/rfcs/`.
Aqui, toda a comunidade (**Especialistas** validando a regra, **Desenvolvedores** avaliando custos técnicos, **Auditores** pontuando riscos) delibera e entra em consenso sobre *como* será construído.

### 3. Desenvolvimento Ativo
Com o RFC unificado e aprovado (Merged), os **Desenvolvedores** "puxam" a tarefa. Criam uma branch (`feature/numero-da-issue`) e escrevem o código referenciando o RFC e a Issue base. O código submetido em PR deve conter cobertura de testes unitários.

### 4. Validação & Estresse (QA)
Os **Testers/Auditores** assumem o controle, submetendo a PR do desenvolvedor à nossa malha de testes severa. Avaliam os critérios de aceite de segurança antes da aprovação do PR.

### 5. Merge e Release
Aprovado por todas as pontas (Negócio, Código e Segurança), um dos Mantenedores do repositório ("Core Approvers") efetua o merge na branch principal. Periodicamente, as consolidações giram o número da versão para as entidades governamentais espelharem.

### 6. Padrões de Pull Request (PR) e Code Review
A qualidade do código do Banco Central não pode ser comprometida. Todo o código submetido via PR passará por um processo de avaliação estrito:
*   **Abertura do PR**: Todo PR deve estar associado a uma Issue ou RFC. A descrição deve deixar claro *o que* foi feito e *como* testar.
*   **Testes Obrigatórios**: O CI/CD bloqueará qualquer PR com cobertura de testes unitários abaixo do limiar (Atualmente: 85%) ou se os testes de integração falharem.
*   **Code Review Assíncrono**: Pelo menos dois (2) Desenvolvedores "Core Tech" precisam revisar a lógica, complexidade ciclomática e aderência à linguagem (ex: *idiomatic Go*).
*   **Security Review**: Se o PR modificar rotas do API Gateway, contratos do Ledger ou fluxos criptográficos do NumoTrust, um "Tester/Auditor" de AppSec deve aprovar explicitamente a arquitetura de segurança.

---

## 🚀 Primeiros Passos (Getting Started)

1. Faça um Fork do repositório para a sua conta.
2. Veja o arquivo de instrução de ambiente local no `README.md`.
3. Navegue até a aba "Issues" e busque pelas *tags* `good first issue` ou `help wanted`.
4. Se apresente na issue comentando que tem interesse em trabalhar nela.
5. Inicie sua contribuição, e seja bem-vindo ao projeto mais importante da economia!

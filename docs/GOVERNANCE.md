# Governança do Projeto Numo

Diante da sua missão de atuar como uma Infraestrutura Pública Digital (DPI) de nível estatal, o Numo adota um modelo evolutivo focado em construir uma **Comunidade Técnica de Liderança Aberta**. Queremos garantir que as decisões sejam tomadas por aqueles que efetivamente constroem o produto, garantindo transparência, neutralidade técnica e sanidade arquitetural. Este documento — guiado pelos princípios do manual *The Open Source Way* — afasta a antiga "meritocracia implícita" para estabelecer canais precisos e previsíveis de decisão, garantindo que Instituições Financeiras, Bancos Centrais e Cidadãos compreendam como o poder flui e se renova no projeto.

## 👥 Papéis na Comunidade (Roles)

Para participar e escalar níveis de acesso no Numo, o caminho (Contributor Ladder) é totalmente auditável:

### 1. Membros (Members)
Qualquer pessoa, instituição representativa ou empresa que utilize ou observe a DPI. Eles não possuem obrigação de submissão de código, mas são a voz primordial de "Demanda do Produto".
*   **Acesso:** Leitura pública.
*   **Privilégios:** Submeter *Issues* de bugs ou *Feature Requests* nos fóruns oficiais.
*   **Deveres:** Seguir o Código de Conduta restrito de comunicação técnica.

### 2. Contribuidores (Contributors)
Pessoas que ativamente submetem melhorias (Código, Documentação, Design, ou Casos de Uso/Negócio). Dividem-se entre Desenvolvedores e Especialistas Financeiros.
*   **Qualificação:** Alcançado após a fusão (*merge*) de sua primeira Pull Request ou Request for Comments (RFC).
*   **Privilégios:** Revisar o código de outros pares (Code Review), ter sua opinião de forma pesada no direcionamento de Features.
*   **Autoridade:** Participar ativamente nas decisões arquiteturais estruturais.

### 3. Líderes (Core Leaders - Em Formação)
Um conselho (inicialmente de 5 cadeiras) responsável por atuar como os *Maintainers* supremos da fundação.
*   **Qualificação:** Eleitos formalmente, seja por longo histórico de arquitetura e consistência no Numo, ou nomeação estatal caso o projeto passe ao controle administrativo de um Banco Central mantenedor.
*   **Privilégios:** Acesso de *Write* no repositório master. Representar o projeto frente à imprensa ou entidades regulatórias globais (`speaking for the project`).
*   **Autoridade Suprema:** Aprovação (Aproval) ou veto técnico final de RFCs estruturais de RTGS (ex: mudanças criptográficas de pacs.008). 

---

## 🏛 Processo de Decisão (The Core Workflow)

As decisões de arquitetura e direção não são feitas de portas fechadas:

1.  **Consenso Rápido (Lazy Consensus):** Para *Pull Requests* de bugfixes e melhorias incrementais, usamos o consenso passivo. Se um *Leader* aprovar e nenhum outro objetar em 48 horas úteis, o código transita para a master.
2.  **Mudanças Estruturais (RFCs):** Toda nova regra de negócio de Compensação ou Criptografia deve ser debatida abertamente através de um "Request For Comments". 
3.  **Votos Formais:** Casos de divergência arquitetural entre *Contributors* exigem resolução pública (maioria simples dos líderes ativos).

## 🔄 Renovação e Saída (Offboarding)
A governança DPI impede pontos únicos de falha. Um *Leader* em hiato ("Inativo" por mais de 6 meses sem prévio aviso de licença) perde voluntária e automaticamente os privilégios de `Write/Maintainer`. Em seu lugar, ocorre a promoção imediata do *Contributor* sênior com mais métricas de aceite recentes.

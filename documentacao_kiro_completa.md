# Documentação Completa do Kiro - Guia Detalhado

**Data da Coleta:** Maio 2026
**Fonte:** Documentação oficial Kiro.dev (https://kiro.dev/docs)

---

## Índice

1. [Visão Geral](#1-visão-geral)
2. [Instalação](#2-instalação)
3. [Autenticação](#3-autenticação)
4. [Funcionalidades Principais](#4-funcionalidades-principais)
   - 4.1 Specs (incluindo Parallel Task Execution, Quick Plan e Analyze Requirements)
   - 4.2 Steering (incluindo Global Steering)
   - 4.3 Hooks
   - 4.4 Powers
   - 4.5 Agente Autônomo
   - 4.6 Agent Skills
   - 4.7 Subagents e Custom Agents (IDE)
   - 4.8 Dev Servers (IDE)
   - 4.9 Custom Agents (CLI)
   - 4.10 Plan Agent (CLI)
   - 4.11 Agent Client Protocol — ACP (CLI)
   - 4.12 Terminal UI (CLI)
   - 4.13 MCP (incluindo Remote MCP, Server Directory e Tool Search)
   - 4.14 Checkpointing
   - 4.15 Multi-root Workspaces
   - 4.16 AST-based Code Navigation and Editing
   - 4.17 IDE Diagnostics Integration
   - 4.18 Semantic Rename e Smart Relocate
   - 4.19 Conversation Compaction (CLI)
   - 4.20 Custom Extension Registry
   - 4.21 Document Attachments
   - 4.22 Hunk-Based Review (Supervised Mode)
   - 4.23 Summarization
   - 4.24 Slash Commands
   - 4.25 Headless Mode (CLI)
   - 4.26 Skills como Slash Commands (CLI)
   - 4.27 Adaptive Thinking
   - 4.28 Kiro Web (Preview)
   - 4.29 Modelos Disponíveis
   - 4.30 Rewind Conversations (CLI)
   - 4.31 Reasoning Effort (CLI)
   - 4.32 Unified Settings Menu (CLI)
   - 4.33 KIRO_HOME e Configurações Avançadas (CLI)
5. [Configuração](#5-configuração)
6. [Acesso Enterprise](#6-acesso-enterprise)
7. [Privacidade e Segurança](#7-privacidade-e-segurança)
8. [Planos e Preços](#8-planos-e-preços)
9. [Benchmark: SWE-PolyBench](#benchmark-swe-polybench)
10. [Recursos Adicionais](#9-recursos-adicionais)

---

## 1. VISÃO GERAL

O Kiro é um IDE agentic desenvolvido pela AWS que auxilia desenvolvedores desde o protótipo até a produção. Diferente de assistentes de código tradicionais que oferecem apenas autocompletar, o Kiro adota uma abordagem agentic com agentes autônomos de IA que podem gerar planos de projeto, criar arquivos, executar testes e atualizar documentação.

O Kiro está disponível em três modalidades:
- **Kiro IDE** — IDE standalone para desktop (macOS, Windows, Linux)
- **Kiro CLI** — Interface de linha de comando para uso em terminais (macOS, Linux, Windows 11 e RHEL)
- **Kiro Web** — Agente de desenvolvimento em navegador (Preview) em [app.kiro.dev](https://app.kiro.dev/), que clona repositórios em sandbox isolado na nuvem e entrega mudanças como pull requests no GitHub

Não é necessário possuir uma conta AWS para utilizar o Kiro.

**Fonte:** [Kiro.dev](https://kiro.dev/) | [Documentação](https://kiro.dev/docs/) | [FAQ](https://kiro.dev/faq/)

---

## 2. INSTALAÇÃO

### 2.1 Instalação do Kiro IDE

Acesse a página de downloads oficial em [kiro.dev/downloads](https://kiro.dev/downloads/) e baixe o instalador para seu sistema operacional. Após a instalação, faça login com um dos métodos de autenticação disponíveis.

**Fonte:** [Instalação IDE](https://kiro.dev/docs/getting-started/installation)

### 2.2 Instalação do Kiro CLI

O Kiro CLI pode ser instalado separadamente para uso via terminal em macOS, Linux e Windows 11.

**macOS / Linux:**
```bash
curl -fsSL https://cli.kiro.dev/install | bash
```

**Windows 11 (PowerShell):**
```powershell
irm 'https://cli.kiro.dev/install.ps1' | iex
```

**Linux — formatos disponíveis:**
- **AppImage** — formato portátil compatível com a maioria das distribuições, incluindo Red Hat Enterprise Linux (RHEL)
- **Zip** — builds padrão (glibc 2.34+) e musl (glibc < 2.34) para x86_64 e aarch64
- **Ubuntu** — pacote `.deb` instalável via `dpkg`

**Atualização automática:** O CLI verifica atualizações em segundo plano. Desative com:
```bash
kiro-cli settings "app.disableAutoupdates" "true"
```

**Proxy corporativo (v1.8.0+):** suporte a `HTTP_PROXY`, `HTTPS_PROXY` e `NO_PROXY`.

**Diagnóstico e desinstalação:**
```bash
kiro-cli doctor
kiro-cli uninstall
```

**Fonte:** [Instalação CLI](https://kiro.dev/docs/cli/installation/)

### 2.3 Acesso ao Kiro Web

O Kiro Web não requer instalação local — acesse diretamente em [app.kiro.dev](https://app.kiro.dev/). Pré-requisitos: assinatura Kiro Pro (ou superior) e conta GitHub conectada. Disponível apenas na região US East (N. Virginia) `us-east-1` durante o Preview.

**Fonte:** [Kiro Web](https://kiro.dev/docs/web/)

---

## 3. AUTENTICAÇÃO

O Kiro oferece múltiplos métodos de autenticação, divididos entre uso individual e uso enterprise/organizacional.

**Fonte:** [Authentication Methods - IDE](https://kiro.dev/docs/getting-started/authentication/) | [Authentication Methods - CLI](https://kiro.dev/docs/cli/authentication)

### 3.1 Métodos para Usuários Individuais

Estes métodos são voltados para desenvolvedores individuais, projetos pessoais ou organizações que não utilizam IAM Identity Center.

#### 3.1.1 Login com GitHub

1. No Kiro, escolha "Sign in with GitHub"
2. Você será redirecionado ao navegador padrão para completar o processo
3. Insira seu nome de usuário ou e-mail e senha do GitHub
4. Escolha "Sign in"
5. Escolha "Authorize kirodotdev" para autorizar o aplicativo Kiro com sua conta GitHub

#### 3.1.2 Login com Google

1. No Kiro, escolha "Sign in with Google"
2. Você será redirecionado ao navegador padrão
3. Selecione ou insira sua conta Google
4. Autorize o acesso ao aplicativo Kiro

#### 3.1.3 Login com AWS Builder ID

O AWS Builder ID é um perfil pessoal que fornece acesso a ferramentas e serviços selecionados da AWS. É gratuito e independente de qualquer conta AWS existente.

1. No Kiro, escolha "Login with AWS Builder ID"
2. Você será redirecionado ao navegador padrão
3. Insira seu endereço de e-mail e escolha "Next"
4. Insira sua senha e escolha "Sign in"
5. Escolha "Allow access" para autorizar o aplicativo Kiro

O AWS Builder ID é separado de qualquer credencial de conta AWS. Você pode usar o mesmo e-mail para o Builder ID e para o usuário root de uma conta AWS, mas são identidades independentes.

### 3.2 Método para Usuários Enterprise

#### 3.2.1 Login com AWS IAM Identity Center (SSO)

Este método é destinado a organizações que gerenciam o acesso de seus desenvolvedores de forma centralizada. Requer que um administrador tenha configurado previamente um perfil Kiro enterprise conectado ao IAM Identity Center.

1. No Kiro, escolha "Sign in with IAM Identity Center"
2. Insira a URL de início (start URL) fornecida pelo administrador da sua organização
3. Você será redirecionado ao navegador para autenticação via SSO corporativo
4. Após autenticação, o acesso é concedido com base nas permissões e assinaturas configuradas pelo administrador

#### 3.2.2 Identity Providers Externos (Okta e Microsoft Entra ID)

Além do IAM Identity Center, o Kiro enterprise suporta integração direta com provedores de identidade externos:

- **Okta** — integração via OIDC (login) + SAML (sincronização SCIM de usuários e grupos)
- **Microsoft Entra ID** — integração via OIDC + SAML com verificação de domínio DNS

Esses provedores permitem que organizações que já utilizam Okta ou Microsoft Entra ID como IdP corporativo conectem seus usuários ao Kiro sem necessidade de migrar para o IAM Identity Center. Os desenvolvedores fazem login com suas credenciais corporativas existentes, e a sincronização de usuários e grupos acontece automaticamente via SCIM.

**Fonte:** [Authentication Methods - IDE](https://kiro.dev/docs/getting-started/authentication/) | [Blog: Enterprise](https://kiro.dev/blog/)

### 3.3 Autenticação no Kiro CLI

O Kiro CLI suporta os mesmos métodos de autenticação, com um fluxo adaptado para o terminal:

1. Execute `kiro-cli` ou `kiro-cli login` no terminal
2. Pressione Enter quando solicitado para completar o login no navegador
3. No navegador, escolha o método de autenticação:
   - Google
   - GitHub
   - Builder ID
   - Sua organização (IAM Identity Center)
4. Após autenticação no navegador, retorne ao terminal — você estará logado

#### 3.3.1 Device Flow (Ambientes Remotos)

Em ambientes remotos (SSH, SSM, contêineres, cloud workspaces), o CLI oferece autenticação por device flow — sem port forwarding. O CLI exibe uma URL e um código único para inserir em qualquer navegador (laptop, celular, etc.).

**Provedores que suportam device flow:** Google, GitHub, AWS Builder ID e IAM Identity Center (provedores externos como Okta e Entra ID ainda não suportam device flow — em desenvolvimento).

**Fluxo:**
1. Executar `kiro-cli login` e escolher o método
2. O CLI exibe URL + código único
3. Abrir a URL em qualquer navegador e inserir o código
4. O CLI detecta o sucesso automaticamente

#### 3.3.2 Autenticação por API Key (Modo Headless)

Para uso em CI/CD e ambientes sem navegador, o CLI aceita autenticação via API key (somente para Pro, Pro+ e Power):

```bash
# macOS/Linux
export KIRO_API_KEY=ksk_xxxxxxxx
kiro-cli chat --no-interactive "seu prompt aqui"
```

```powershell
# Windows
$env:KIRO_API_KEY = "ksk_xxxxxxxx"
kiro-cli chat --no-interactive "seu prompt aqui"
```

**Precedência de credenciais:**
1. Sessão ativa via `kiro-cli login`
2. Variável `KIRO_API_KEY`
3. Sem credenciais — o CLI solicita login

API keys são criadas em [app.kiro.dev](https://app.kiro.dev/) na seção API Keys. O valor completo aparece apenas no momento da criação. Trate-as como credenciais de longa duração: armazene como secret, rotacione regularmente e revogue quando comprometidas.

**Comandos relacionados:**
- `kiro-cli whoami` — mostra o método de autenticação ativo
- `kiro-cli logout` — encerra a sessão

**Fonte:** [CLI Authentication](https://kiro.dev/docs/cli/authentication/)

### 3.4 Comparativo dos Métodos de Autenticação

| Método | Tipo de Uso | Requer Conta AWS | Gerenciamento Centralizado |
|--------|-------------|------------------|---------------------------|
| GitHub | Individual | Não | Não |
| Google | Individual | Não | Não |
| AWS Builder ID | Individual | Não | Não |
| IAM Identity Center | Enterprise | Sim (admin) | Sim |
| Okta (via IdP) | Enterprise | Sim (admin) | Sim |
| Microsoft Entra ID (via IdP) | Enterprise | Sim (admin) | Sim |

---

## 4. FUNCIONALIDADES PRINCIPAIS

### 4.1 Specs (Especificações)

Specs são artefatos estruturados que formalizam o processo de desenvolvimento de funcionalidades complexas. Fornecem uma abordagem sistemática para transformar ideias de alto nível em planos de implementação detalhados com rastreamento e responsabilidade claros.

Specs são úteis quando você precisa pensar profundamente em uma funcionalidade, planejar refatorações, ou entender o comportamento de sistemas. Elas guiam os agentes de IA a melhores implementações ao tornar suposições explícitas e garantir clareza nos requisitos.

- Suportam referências a arquivos adicionais via `#[[file:<nome_arquivo>]]` (incluindo line ranges: `#[[file:src/utils/helper.ts:10-25]]`)
- Documentos como OpenAPI spec ou GraphQL spec podem influenciar a implementação
- Projetadas para refinamento contínuo conforme o projeto evolui
- É possível referenciar specs no chat usando `#spec` para obter respostas alinhadas com a especificação

O Kiro oferece três tipos de specs, cada um para um cenário diferente:

**Fonte:** [Specs](https://kiro.dev/docs/specs/)

#### 4.1.1 Feature Specs — Requirements-first (Requisitos primeiro)

O fluxo tradicional de desenvolvimento orientado a specs, construído em torno do fluxo PM/engenharia: requisitos primeiro, depois design, depois tarefas. Ideal para projetos novos (greenfield) onde as opções estão abertas.

**Fluxo em 3 fases:**

1. **Requirements (Requisitos)** — O Kiro analisa seu prompt e gera requisitos detalhados baseados em user stories, usando o formato EARS (Easy Approach to Requirements Syntax): `WHEN [condição] THE SYSTEM SHALL [comportamento esperado]`. Expande pedidos vagos e destaca edge cases.
2. **Design (Design técnico)** — O Kiro cria documentação arquitetural detalhada incluindo componentes do sistema, interfaces e estratégias de implementação.
3. **Tasks (Tarefas)** — Lista priorizada de tarefas de implementação que o agente executa sequencialmente.

Funciona quando você entende os comportamentos e resultados necessários, mas o caminho técnico ainda não está claro. Você está explorando "o que isso deve fazer?" antes de "como deve funcionar?".

**Quando escolher Requirements-first:**
- Você conhece o comportamento do sistema que quer construir
- A arquitetura é flexível e pode ser desenhada para atender às necessidades
- Está construindo features de produto orientadas por feedback de clientes
- Começando sem restrições técnicas

**Fonte:** [Feature Specs — Requirements-first](https://kiro.dev/docs/specs/feature-specs/requirements-first/)

#### 4.1.2 Feature Specs — Tech Design-first (Design técnico primeiro)

Para cenários onde você já tem uma visão técnica — por experiência, restrições arquiteturais ou prototipagem — e precisa trabalhar de trás para frente para formalizar o que o sistema realmente realiza. Ideal para construir funcionalidades em cima de aplicações existentes (brownfield), onde você precisa trabalhar dentro da arquitetura e stack tecnológico atuais.

**Fluxo:**

1. **Design** — Ao criar uma Feature Spec, escolha "tech Design-first". Selecione o nível de detalhe: design de alto nível (diagramas de sistema e componentes) ou design de baixo nível (algoritmos e assinaturas de funções). O Kiro gera o documento de design primeiro.
2. **Requirements** — Após iterar e aprovar o design, o Kiro deriva os requisitos a partir do design, garantindo que sejam viáveis.
3. **Tasks** — O restante do fluxo segue igual: tarefas, implementação e property-based testing.

**Quando escolher Design-first:**
- Você tem um design técnico ou arquitetura existente
- O sistema deve atender requisitos não-funcionais rígidos (latência, throughput, compliance)
- Está prototipando com um stack tecnológico específico
- Explorando viabilidade técnica antes de definir escopo

**Importação de designs existentes:** Você pode fazer upload de diagramas de arquitetura (PNG, JPG), colar conteúdo de design, ou usar integração MCP com ferramentas de design. O Kiro formaliza o design em `design.md` e deriva requisitos a partir da arquitetura.

**Fonte:** [Feature Specs — Tech Design-first](https://kiro.dev/docs/specs/feature-specs/tech-design-first/)

#### 4.1.3 Bugfix Specs

Bugfix Specs modelam como desenvolvedores experientes abordam correções de bugs: identificar a causa raiz, entender o que deve mudar, e preservar explicitamente o que não deve. Fornecem uma abordagem estruturada que guia através de análise de causa raiz, design da correção e prevenção de regressões.

**Benefícios principais:**
- **Correções cirúrgicas** — restrições explícitas garantem que apenas mudanças necessárias sejam feitas
- **Prevenção de regressões** — comportamento inalterado é documentado e testado
- **Documentação** — registro completo do bug, correção e raciocínio para referência futura
- **Confiabilidade** — workflow estruturado previne armadilhas comuns de correções ad-hoc

**Quando usar Bugfix Specs:**
- Bugs complexos que requerem análise de causa raiz
- Bugs em caminhos críticos de código onde regressões são custosas
- Bugs que precisam de documentação para compliance ou conhecimento da equipe
- Situações onde tentativas anteriores de correção causaram regressões

**Fluxo em 3 fases (mesmo workflow de Feature Specs, com conteúdo adaptado):**

1. **Bugfix Analysis (Análise do bug)** — Ao invés de um documento de requisitos, você cria um `bugfix.md` que captura:
   - **Current Behavior (Comportamento atual/Defeito)** — WHEN [condição] THEN o sistema [comportamento incorreto]
   - **Expected Behavior (Comportamento esperado/Correto)** — WHEN [condição] THEN o sistema SHALL [comportamento correto]
   - **Unchanged Behavior (Prevenção de regressão)** — WHEN [condição] THEN o sistema SHALL CONTINUE TO [comportamento existente]

2. **Design** — O Kiro explora o codebase para identificar a causa raiz e gera um `design.md` com:
   - Análise de causa raiz
   - Abordagem proposta para a correção
   - Propriedades a testar: implementação atual produz comportamento incorreto (valida que o bug existe), implementação corrigida produz comportamento correto (valida que a correção funciona), implementação inalterada continua funcionando (previne regressões)

3. **Tasks** — Tarefas de implementação com property-based tests (PBTs) que validam: o bug é reproduzível, o bug é corrigido, e nenhuma regressão é introduzida.

**Como começar:**
1. Escolha Spec no painel de chat
2. Descreva o bug, incluindo: quando ocorre (passos de reprodução), o que deveria acontecer, e quaisquer restrições (código que não deve ser modificado)
3. Escolha Bugfix quando o Kiro perguntar qual é sua intenção
4. Siga o workflow através de análise, design e implementação

**Quando usar Bugfix Spec vs. correção rápida:** Use Bugfix Spec para bugs em caminhos críticos, quando tentativas anteriores causaram regressões, quando a causa raiz não é imediatamente óbvia, ou quando é necessária documentação. Uma correção rápida no chat é suficiente para problemas simples como typos, erros de lógica simples ou mudanças de uma linha.

**Fonte:** [Bugfix Specs](https://kiro.dev/docs/specs/bugfix-specs/) | [Best Practices](https://kiro.dev/docs/specs/best-practices/#bugfix-specs)

#### 4.1.4 Correctness — Property-Based Testing (PBT)

"Spec correctness" ajuda a responder uma pergunta fundamental: sua implementação realmente faz o que você especificou? Quando IA gera código, como você sabe que ele corresponde à sua intenção?

Property-Based Testing representa uma mudança na forma de pensar sobre corretude com IA, passando de verificar exemplos individuais para validar propriedades universais em espaços inteiros de input. Testes unitários tradicionais verificam apenas exemplos específicos, e quem os escreve — humano ou IA — é limitado por seus próprios vieses. Ao traduzir automaticamente especificações em linguagem natural em propriedades executáveis e gerar casos de teste abrangentes, o Kiro cria um loop de feedback que ajuda tanto agentes de IA quanto desenvolvedores humanos a construir software mais confiável.

**O que é uma propriedade:**
Uma propriedade é uma declaração universal sobre como seu sistema deve se comportar. No mundo de especificações do Kiro, isso mapeia diretamente para requisitos EARS: "Para qualquer usuário autenticado e qualquer listagem ativa, o usuário pode visualizar essa listagem."

**Como PBT funciona (exemplo de app de venda de carros):**
- Teste tradicional: Usuário adiciona Carro #5 aos favoritos, Carro #5 aparece na lista
- Teste PBT: Para qualquer usuário e qualquer carro, WHEN o usuário adiciona o carro aos favoritos, THE System SHALL exibi-lo na lista

O PBT testa automaticamente com Usuário A adicionando Carro #1, Usuário B adicionando Carro #500, usuários com caracteres especiais nos nomes, carros com vários status, e centenas de combinações — capturando edge cases e verificando que a implementação corresponde à intenção.

**Workflow integrado com Specs:**

1. **Extração de propriedades** — O Kiro extrai propriedades dos requisitos EARS e determina quais podem ser testadas logicamente
2. **Fase de design** — Propriedades são geradas e vinculadas aos requisitos originais e tarefas
3. **Execução de tarefas** — PBTs são opcionais por padrão, permitindo focar na implementação core primeiro. Quando executados, geram centenas ou milhares de casos de teste aleatórios
4. **Análise de falhas** — Quando um teste falha, o Kiro identifica o cenário específico. Você pode conversar com o Kiro para entender a falha e determinar a correção apropriada — seja atualizar a implementação, ajustar o teste, ou refinar o requisito

**Shrinking:** Quando um teste falha, o framework automaticamente reduz o contraexemplo ao caso mínimo que reproduz a falha — quase como um red team tentando quebrar seu código.

**Frameworks suportados:**
- **fast-check** para TypeScript/JavaScript
- **Hypothesis** para Python

**Formas comuns de propriedades:**
- **Invariantes** — condições que devem ser sempre verdadeiras (ex: tamanho de lista nunca negativo)
- **Round-trip** — operações inversas que devem retornar ao estado original (ex: encode/decode)
- **Idempotência** — aplicar a mesma operação múltiplas vezes produz o mesmo resultado

**Caso real de segurança:** Em um cenário documentado, PBT identificou uma vulnerabilidade de prototype pollution (`__proto__`) em código JavaScript. O teste gerou automaticamente inputs contendo chaves como `__proto__` e `constructor`, detectando que propriedades maliciosas podiam ser injetadas no prototype chain de objetos — uma falha que testes baseados em exemplos dificilmente encontrariam.

**Fonte:** [Correctness with Property-based Tests](https://kiro.dev/docs/specs/correctness/) | [Blog: Property-Based Testing](https://kiro.dev/blog/)

#### 4.1.5 Parallel Task Execution e Run All Tasks

O Kiro permite executar todas as tarefas de uma spec com um único clique no botão **Run all Tasks** do arquivo `tasks.md`. Desde o IDE 0.12, a execução é **paralela**: tarefas independentes rodam concorrentemente em vez de uma por vez.

**Como funciona (modelo de ondas/waves):**
- O Kiro constrói um **grafo de dependências** a partir das tarefas em `tasks.md`
- **Wave 1** — todas as tarefas sem dependências executam concorrentemente
- **Wave 2** — tarefas cujas dependências foram satisfeitas pela Wave 1 executam concorrentemente
- O ciclo continua até todas as tarefas serem concluídas
- Cada tarefa executa em seu próprio contexto isolado
- Ondas rodam sequencialmente; tarefas dentro de uma onda rodam em paralelo

**Ganhos de performance:** para specs com **4 ou mais tarefas independentes**, a execução paralela pode ser **até 4x mais rápida** que a sequencial. Não há configuração — basta clicar em Run all Tasks e o Kiro analisa automaticamente as dependências.

**Fonte:** [Specs — Running Tasks in Parallel](https://kiro.dev/docs/specs/#running-tasks-in-parallel) | [Changelog IDE 0.12](https://kiro.dev/changelog/ide/0-12/)

#### 4.1.6 Quick Plan — Spec em passagem única

Quick Plan é um modo de sessão de Spec que gera `requirements.md`, `design.md` e `tasks.md` em uma **única passagem**, sem os portões de aprovação entre as fases. Em vez de revisar e aprovar cada artefato, você antecipa o contexto respondendo a perguntas de clarificação logo no início e chega direto a uma lista de tarefas acionáveis.

**Como criar:** a partir do botão `+` em Specs no painel do Kiro, ou via Spec no painel de chat — o seletor de tipo oferece Feature Specs, Bugfix Specs e **Quick Plan**.

**Fluxo:**
1. O Kiro faz perguntas de clarificação iniciais sobre escopo, restrições e casos de borda
2. Gera os três artefatos em sequência, sem portões de aprovação
3. Você aterrissa direto na lista de tarefas
4. Os artefatos ficam salvos em `.kiro/specs/` no mesmo formato de uma Spec padrão, permitindo continuar qualquer fluxo, regerar tarefas ou referenciar com `#spec`

**Quando usar:**
- Funcionalidades bem compreendidas, onde você confia na saída do Kiro
- Prototipagem rápida, quando velocidade importa mais que revisão
- Features similares a outras que você já construiu

**Quando evitar:** territórios desconhecidos, requisitos que precisam de iteração, domínios sensíveis a compliance ou sistemas de alto risco — nesses casos, use Feature Spec padrão com portões de aprovação.

**Diferença vs. Vibe mode:** Vibe mode é conversacional e não salva artefatos em `.kiro/specs/`. Quick Plan produz todos os artefatos completos, apenas sem portões.

**Fonte:** [Quick Plan](https://kiro.dev/docs/specs/quick-plan/)

#### 4.1.7 Analyze Requirements — Análise profunda de requisitos

Analyze Requirements é um passo de análise profunda que detecta inconsistências lógicas, ambiguidades, restrições conflitantes e lacunas nos requisitos **antes** de avançar para o design. Usa raciocínio automatizado sobre o conjunto completo de requisitos (não isoladamente) para encontrar problemas difíceis de pegar em uma leitura manual.

**O que a análise detecta:**
- **Inconsistências lógicas** — dois requisitos que individualmente fazem sentido, mas juntos são impossíveis
- **Ambiguidades** — expressões como "arquivos grandes" ou "tempos de resposta rápidos" que levariam a implementações divergentes
- **Restrições conflitantes** — requisitos funcionais e não-funcionais incompatíveis
- **Pressupostos não declarados** — referências a conceitos ou comportamentos não definidos
- **Casos de borda ausentes** — modos de falha, condições de fronteira e cenários concorrentes não cobertos

**Como invocar:** após os requisitos serem gerados, Analyze Requirements aparece em dois lugares — no chat, junto das opções de como prosseguir, e no dropdown **Continue** do editor, ao lado de **Proceed to Design**.

**O que esperar:**
- A análise leva **minutos, não segundos** — raciocínio cross-requirement é mais intensivo que operações típicas
- Os achados chegam por streaming no chat como perguntas de clarificação com: requisitos envolvidos, explicação do problema em linguagem simples e sugestões de correção selecionáveis
- É possível responder com texto customizado ou descartar a pergunta se a ambiguidade for intencional
- Ao resolver as perguntas, o Kiro atualiza `requirements.md` no editor

**Quando usar:**
- Funcionalidades complexas com muitos requisitos
- Projetos sensíveis a domínio (finanças, saúde, compliance)
- Sessões de Quick Plan onde os requisitos foram auto-gerados sem revisão manual
- Pode ser re-executada após edições — o Kiro reanalisa os requisitos afetados e suas interações

**Fonte:** [Analyze Requirements](https://kiro.dev/docs/specs/analyze-requirements/)

#### 4.1.8 Melhores Práticas para Specs

##### Escolhendo o Workflow

| Workflow | Quando Usar |
|----------|-------------|
| Requirements-first | Comportamento do sistema conhecido, arquitetura flexível, features orientadas por feedback, sem restrições técnicas |
| Design-first | Design técnico existente, requisitos não-funcionais rígidos, prototipagem com stack específico, exploração de viabilidade |

Não é possível trocar de workflow após iniciar uma spec. Se necessário, crie uma nova spec com o workflow desejado e copie conteúdo relevante.

##### Iterando em Feature Specs

Para Requirements-first:
1. Modifique `requirements.md` diretamente ou peça ao Kiro para adicionar novos requisitos
2. Navegue até `design.md` e selecione "Refine" para atualizar design e tarefas
3. Navegue até `tasks.md` e escolha "Update tasks" para criar novas tarefas

Para Design-first:
1. Modifique `design.md` diretamente ou peça ao Kiro para atualizá-lo
2. Após mudanças na arquitetura, peça ao Kiro para validar e regenerar requisitos
3. Navegue até `tasks.md` e escolha "Update tasks"

##### Importando Requisitos Existentes

Se seus requisitos já existem em outro sistema (JIRA, Confluence, Word):
- **Via MCP:** Se a ferramenta tem um servidor MCP, conecte diretamente para importar
- **Manual:** Copie os requisitos para um arquivo no repo (ex: `foo-prfaq.md`) e diga ao Kiro: `#foo-prfaq.md Generate a spec from it`

##### Tarefas MVP

Durante a criação de specs, você pode escolher "Keep optional tasks (faster MVP)" para marcar testes e documentação como opcionais (✱), ou "Make all tasks required" para cobertura completa desde o início. Tarefas opcionais permanecem visíveis para execução posterior.

##### Tarefas já implementadas

Se algumas tarefas já foram implementadas:
- Clique em "Update tasks" no `tasks.md` — o Kiro marca automaticamente tarefas completas
- Ou peça ao Kiro em uma sessão de spec: "Check which tasks are already complete"

##### Referenciando Specs no Chat

Use `#spec` no chat para incluir todos os arquivos da spec (requirements.md, design.md, tasks.md) no contexto da conversa. Exemplos:
```
#spec:user-authentication implement task 2.3
#spec:user-authentication update the design file to include password reset flow
#spec:user-authentication does my current implementation meet the acceptance criteria for task 7.1?
```

##### Iniciando Spec a partir de Vibe Session

Você pode ter uma conversa vibe e depois dizer `Generate spec`. O Kiro perguntará se deseja iniciar uma sessão de spec e gerará requisitos baseados no contexto da conversa.

##### Organizando Specs

Recomenda-se criar múltiplas specs para diferentes features ao invés de uma única spec para todo o codebase:
```
.kiro/specs/
├── user-authentication/       # Login, signup, password reset
├── product-catalog/           # Product listing, search, filtering
├── shopping-cart/             # Add to cart, quantity updates, checkout
├── payment-processing/        # Payment gateway integration
└── admin-dashboard/           # Product management, user analytics
```

**Fonte:** [Best Practices](https://kiro.dev/docs/specs/best-practices/)

#### Resumo dos Tipos de Spec

| Tipo | Quando Usar | Fluxo |
|------|-------------|-------|
| Feature — Requirements-first | Projetos novos, opções abertas | Requisitos → Design → Tarefas |
| Feature — Tech Design-first | Aplicações existentes, arquitetura definida | Design → Requisitos → Tarefas |
| Quick Plan | Features bem compreendidas, prototipagem rápida | Requisitos + Design + Tarefas em passagem única |
| Bugfix | Correção de bugs, precisão cirúrgica | Comportamento atual/esperado/inalterado → Design → Tarefas |

### 4.2 Steering (Direcionamento)

Steering permite incluir contexto e instruções adicionais nas interações com o Kiro. Localizado em `.kiro/steering/*.md`, pode ser:

- **Sempre incluído** (`always`) — comportamento padrão, carregado em todas as interações
- **Automático** (`auto`) — ativado automaticamente quando relevante para o contexto
- **Condicional por arquivo** (`fileMatch`) — ativado quando um arquivo correspondente ao padrão é lido no contexto (configurado via frontmatter `fileMatchPattern`)
- **Manual** (`manual`) — fornecido pelo usuário via contexto (`#` no chat ou slash commands)

Usos comuns: padrões de equipe, informações do projeto, instruções de build/test.

Steering files suportam referências a arquivos adicionais via `#[[file:<nome_arquivo>]]`, permitindo que documentos como OpenAPI spec ou GraphQL spec influenciem a implementação.

#### Global Steering

Além do steering por workspace, o Kiro suporta Global Steering em `~/.kiro/steering/`, que se aplica a todos os projetos abertos no Kiro. Steering de workspace (`.kiro/steering/`) tem precedência sobre global quando há conflito.

**Casos de uso ideais para Global Steering:**
- Estilo de código pessoal e preferências de formatação
- Filosofia de testes (ex: sempre usar TDD, preferir integration tests)
- Requisitos de segurança padrão (ex: sempre validar inputs, nunca logar PII)
- Padrões de documentação (ex: sempre incluir JSDoc, docstrings obrigatórias)

**Distribuição em equipes:** Global steering pode ser distribuído para toda a equipe via repositório Git compartilhado (clonado em `~/.kiro/steering/`) ou via ferramentas de MDM como Jamf (macOS) ou Intune (Windows) para deployment automatizado.

**Suporte a AGENTS.md:** O Kiro suporta o padrão [AGENTS.md](https://agents.md/) para definir guidelines, padrões de código e padrões arquiteturais. Adicione um arquivo AGENTS.md ao diretório global de steering (`~/.kiro/steering/`) ou à raiz do workspace, e o Kiro o carregará automaticamente.

**Botão "Refine":** O Kiro oferece um botão "Refine" que analisa e otimiza steering files automaticamente, melhorando a clareza e eficácia das instruções para o agente.

**Fonte:** [Steering](https://kiro.dev/docs/steering/) | [Blog: Global Steering](https://kiro.dev/blog/)

### 4.3 Hooks (Gatilhos)

Agent hooks são ferramentas de automação que executam ações predefinidas do agente quando eventos específicos ocorrem no IDE. Eliminam a necessidade de solicitar manualmente tarefas rotineiras e garantem consistência no codebase.

**Fonte:** [Hooks](https://kiro.dev/docs/hooks/) | [Hook Types](https://kiro.dev/docs/hooks/types/) | [Hook Actions](https://kiro.dev/docs/hooks/actions/)

#### Como Funcionam

O sistema de hooks segue um processo de dois passos:
1. **Detecção de evento** — o sistema monitora eventos específicos no IDE
2. **Ação automatizada** — quando um evento ocorre, uma ação (prompt para o agente ou comando shell) é executada

#### Criando Hooks

Hooks podem ser criados de duas formas:
- **Ask Kiro to create a hook** — descreva o hook em linguagem natural e o Kiro gera a configuração
- **Manually create a hook** — preencha um formulário com título, descrição, evento, ação e instruções

Também é possível abrir a UI de hooks via Command Palette: `Cmd + Shift + P` (Mac) / `Ctrl + Shift + P` (Windows/Linux) e digitar `Kiro: Open Kiro Hook UI`.

#### Tipos de Eventos (Triggers)

| Evento | Descrição | Casos de Uso |
|--------|-----------|-------------|
| **Prompt Submit** | Quando o usuário envia um prompt | Fornecer contexto adicional, bloquear prompts, logging |
| **Agent Stop** | Quando o agente completa sua resposta | Compilar código, formatar código gerado, revisar mudanças |
| **Pre Tool Use** | Antes do agente invocar uma ferramenta | Bloquear ferramentas, fornecer instruções adicionais |
| **Post Tool Use** | Após o agente invocar uma ferramenta | Logging, formatação, instruções adicionais |
| **File Save** | Quando arquivos são salvos | Linting, formatação, atualização de arquivos relacionados |
| **File Create** | Quando novos arquivos são criados | Gerar boilerplate, adicionar headers de licença |
| **File Delete** | Quando arquivos são deletados | Limpar arquivos relacionados, atualizar imports |
| **Pre Task Execution** | Antes de uma tarefa de spec iniciar | Setup scripts, validar pré-requisitos |
| **Post Task Execution** | Após uma tarefa de spec completar | Rodar testes, linting, notificar sistemas externos |
| **Manual Trigger** | Executado manualmente pelo usuário | Code reviews on-demand, geração de documentação, security scanning |

#### Filtros para Pre/Post Tool Use

No campo Tool name, é possível especificar categorias built-in ou filtros por prefixo:
- `read`, `write`, `shell`, `web`, `spec` — categorias de ferramentas built-in
- `*` — todas as ferramentas (built-in e MCP)
- `@mcp` — todas as ferramentas MCP
- `@powers` — todas as ferramentas de Powers
- `@builtin` — todas as ferramentas built-in
- Prefixos com `@` são matched por regex (ex: `@mcp.*sql.*` para ferramentas MCP específicas)

#### Variável de Ambiente para Prompt Submit

Quando usando a ação Shell Command com o trigger Prompt Submit, o prompt do usuário pode ser acessado via variável de ambiente `USER_PROMPT`.

#### Ações Disponíveis

| Ação | Descrição | Consumo de Créditos |
|------|-----------|-------------------|
| **Agent Prompt (Ask Kiro)** | Envia um prompt ao agente em linguagem natural | Sim (dispara novo loop do agente) |
| **Shell Command (Run Command)** | Executa um comando shell localmente | Não |

**Comportamento do Shell Command:**
- Exit code 0 (sucesso): stdout é adicionado ao contexto do agente
- Qualquer outro exit code: stderr é enviado ao agente, e para Pre Tool Use o uso da ferramenta é bloqueado; para Prompt Submit, o envio do prompt é bloqueado
- Timeout padrão: 60 segundos (configurável, 0 para desabilitar)

**Nota sobre Prompt Submit:** A ação Agent Prompt neste trigger é chamada "Add to prompt" — o prompt do hook é anexado ao prompt do usuário, e o prompt combinado é enviado ao agente.

#### Melhores Práticas para Hooks

- Escreva instruções detalhadas e sem ambiguidade para ações de Agent Prompt
- Foque em uma tarefa específica por hook
- Teste hooks com cenários de exemplo antes de implantar
- Para hooks de arquivo, comece com padrões limitados antes de expandir
- Valide inputs e considere edge cases
- Documente o propósito de cada hook e armazene configurações em controle de versão
- Revise e atualize hooks regularmente conforme o projeto evolui

**Fonte:** [Hooks](https://kiro.dev/docs/hooks/) | [Best Practices](https://kiro.dev/docs/hooks/best-practices/) | [Examples](https://kiro.dev/docs/hooks/examples/)

### 4.4 Powers (Poderes)

Powers fornecem ao agente de IA acesso instantâneo a conhecimento especializado para qualquer tecnologia. Empacotam ferramentas, fluxos de trabalho e melhores práticas em um formato que o Kiro pode ativar sob demanda. Quando palavras-chave relevantes são mencionadas, o Kiro carrega o contexto e as ferramentas do power automaticamente.

#### Arquitetura de um Power

Um Power é um bundle unificado que empacota três componentes:
- **MCP tools** — servidores MCP que fornecem ferramentas especializadas (ex: API do Postman, CLI do Stripe)
- **POWER.md** — arquivo de steering com frontmatter YAML contendo keywords, descrição e instruções de uso
- **Hooks adicionais** — automações específicas do power (ex: validar schema após edição)

#### Carregamento Dinâmico de Contexto

Powers utilizam carregamento dinâmico baseado em keywords. O Kiro só ativa um power quando detecta palavras-chave relevantes na conversa ou no contexto do projeto. Isso mantém o contexto do agente enxuto — ao invés de carregar dezenas de ferramentas de todos os powers instalados, apenas as ferramentas relevantes são carregadas sob demanda.

#### Estrutura de um Power

```
my-power/
├── POWER.md          # Frontmatter com keywords + instruções de steering
├── mcp.json          # Configuração de servidores MCP
├── steering/         # Steering files adicionais (opcionais)
│   └── workflow.md
└── hooks/            # Hooks específicos do power (opcionais)
    └── on-edit.md
```

#### Instalação

- **Um clique via IDE** — Powers podem ser instalados diretamente pela interface do Kiro IDE
- **Um clique via web** — Botão "Add to Kiro" em páginas web para instalação instantânea
- **Importação do GitHub** — Powers podem ser importados de repositórios GitHub públicos ou privados
- **Diretórios locais** — Powers podem ser carregados de diretórios locais para desenvolvimento e teste

#### Parceiros de Lançamento

O ecossistema de Powers foi lançado com parceiros que oferecem powers oficiais:
- **Datadog** — monitoramento e observabilidade
- **Dynatrace** — observabilidade e performance
- **Figma** — design e prototipagem
- **Neon** — banco de dados serverless Postgres
- **Netlify** — deploy e hosting
- **Postman** — testes e documentação de APIs
- **Supabase** — backend-as-a-service
- **Stripe** — pagamentos e billing
- **Strands Agent** — framework de agentes de IA

#### Cross-Compatibility

Powers são projetados com cross-compatibility em mente. Há planos para suporte em outras ferramentas de desenvolvimento como Cline, Cursor e Claude Code, permitindo que um mesmo power funcione em múltiplos ambientes de desenvolvimento.

**Fonte:** [Powers](https://kiro.dev/docs/powers/) | [Blog: Powers](https://kiro.dev/blog/)

### 4.5 Agente Autônomo (Preview)

O Kiro autonomous agent está atualmente em Preview e integra exclusivamente com o GitHub. Ele trabalha de forma independente em tarefas de desenvolvimento, desde implementação de funcionalidades até correção de bugs, operando de forma assíncrona em ambientes sandbox isolados.

#### Características Principais
- Opera de forma assíncrona — você não precisa ficar esperando
- Aprende com seus code reviews e constrói entendimento profundo do codebase
- Pode trabalhar em múltiplos repositórios em uma única tarefa
- Cria branches e abre pull requests automaticamente no GitHub
- Requer permissões de escrita nos repositórios

#### Como Usar
1. Acesse [app.kiro.dev/agent](https://app.kiro.dev/agent)
2. Conecte sua conta GitHub e instale o Kiro Agent app
3. Selecione os repositórios desejados (opcionalmente)
4. Descreva a tarefa em linguagem natural
5. O agente cria a tarefa, trabalha no sandbox e abre PRs quando concluído

Você pode conversar com o agente a qualquer momento para fazer perguntas, discutir abordagens ou fornecer contexto. Uma vez criada uma tarefa em um chat, não é possível criar uma segunda tarefa no mesmo chat.

> **Aviso:** Selecione apenas repositórios confiáveis, especialmente ao misturar repos públicos e privados, pois o agente aprenderá e seguirá instruções no código do repositório, mesmo que sejam maliciosas.

#### Sandbox do Agente
Cada tarefa executa em seu próprio sandbox isolado com controles de acesso configuráveis:

- **Dockerfile** — o agente procura um Dockerfile na raiz do repositório para configurar o ambiente automaticamente
- **Variáveis de ambiente** — secrets são criptografados em repouso e expostos como variáveis de ambiente no sandbox durante a execução
- **MCP** — configuração MCP é carregada no sandbox e disponível durante a execução da tarefa

#### Modos de Operação no IDE
O agente no IDE opera em dois modos:
- **Autopilot** — modifica arquivos no workspace de forma autônoma
- **Supervised** — permite ao usuário revisar e aceitar/rejeitar alterações (agora com revisão por hunk — ver seção 4.22)

**Fontes:**
- [Kiro Autonomous Agent](https://kiro.dev/docs/autonomous-agent/)
- [Using the Agent](https://kiro.dev/docs/autonomous-agent/using-the-agent/)
- [Agent Setup](https://kiro.dev/docs/autonomous-agent/setup/)
- [Sandbox](https://kiro.dev/docs/autonomous-agent/sandbox)

### 4.6 Agent Skills

O Kiro suporta o padrão aberto Agent Skills ([agentskills.io](https://agentskills.io)), permitindo importar skills da comunidade ou de outras ferramentas de IA compatíveis, e compartilhar suas próprias skills pelo ecossistema.

Skills são pacotes portáveis de instruções que seguem o padrão aberto. Empacotam instruções, scripts e templates em pacotes reutilizáveis que o Kiro ativa quando relevantes para a tarefa.

#### Como Skills Funcionam — Progressive Disclosure

Agentes de IA são cada vez mais capazes, mas frequentemente carecem do contexto específico necessário para trabalho real. Carregar todo o contexto antecipadamente não é prático — muita informação sobrecarrega o agente. Skills resolvem isso com progressive disclosure:

1. **Discovery** — Na inicialização, o Kiro carrega apenas o nome e descrição de cada skill
2. **Activation** — Quando seu pedido corresponde à descrição de uma skill, o Kiro carrega as instruções completas
3. **Execution** — O Kiro segue as instruções, carregando scripts ou arquivos de referência apenas quando necessário

#### Usando Skills

- **Automática:** O Kiro ativa skills automaticamente quando seu pedido corresponde à descrição
- **Slash command:** Digite `/` no input do chat para ver skills disponíveis como slash commands
- **Gerenciamento:** Visualize e gerencie skills na seção "Agent Steering & Skills" no painel do Kiro

#### Escopo de Skills

| Escopo | Localização | Aplicação |
|--------|-------------|-----------|
| **Workspace** | `.kiro/skills/` | Apenas o workspace específico |
| **Global** | `~/.kiro/skills/` | Todos os workspaces |

Em caso de conflito de nomes, a skill do workspace tem prioridade sobre a global.

#### Importando Skills

1. Abra a seção "Agent Steering & Skills" no painel do Kiro
2. Clique em + e selecione "Import a skill"
3. Escolha a fonte:
   - **GitHub** — importe de um repositório público (URL apontando para a pasta da skill ou diretamente para o `SKILL.md`)
   - **Local folder** — importe do sistema de arquivos

#### Criando uma Skill

Uma skill é uma pasta contendo um arquivo `SKILL.md`:

```
my-skill/
├── SKILL.md           # Obrigatório
├── scripts/           # Código executável (opcional)
├── references/        # Documentação (opcional)
└── assets/            # Templates (opcional)
```

**Formato do SKILL.md:**
```markdown
---
name: pr-review
description: Review pull requests for code quality, security issues, and test coverage. Use when reviewing PRs or preparing code for review.
---

## Review process
1. Check for security vulnerabilities
2. Verify error handling
3. Confirm test coverage
4. Review naming and structure
```

**Campos do frontmatter:**

| Campo | Obrigatório | Descrição |
|-------|-------------|-----------|
| name | Sim | Deve corresponder ao nome da pasta. Minúsculas, números, hífens (máx 64 chars) |
| description | Sim | Quando usar esta skill. O Kiro compara com seus pedidos (máx 1024 chars) |
| license | Não | Nome da licença ou referência a arquivo de licença |
| compatibility | Não | Requisitos de ambiente (ex: ferramentas necessárias, acesso à rede) |
| metadata | Não | Dados adicionais como autor ou versão |

#### Diferenças entre Skills, Steering e Powers

| Aspecto | Skills | Steering | Powers |
|---------|--------|----------|--------|
| Padrão | Aberto (agentskills.io) | Específico do Kiro | Específico do Kiro |
| Carregamento | On-demand | always/auto/fileMatch/manual | Dinâmico por keywords |
| Inclui scripts | Sim | Não | Não (mas inclui MCP tools) |
| Uso ideal | Workflows reutilizáveis para compartilhar | Padrões e convenções do projeto | Integrações com ferramentas + guidance |

> **Dica:** Para integrações MCP, Powers geralmente são mais adequados — empacotam ferramentas com guidance built-in e ativam automaticamente baseado no contexto.

**Fonte:** [Agent Skills](https://kiro.dev/docs/skills/) | [Agent Skills Specification](https://agentskills.io/specification)

### 4.7 Subagents e Custom Agents (IDE)

Subagents permitem ao Kiro executar múltiplas tarefas em paralelo ou delegar tarefas específicas a agentes especializados. O Kiro lança subagents automaticamente quando apropriado, ou você pode solicitar manualmente via prompt (ex: "Rode subagents para...").

**Fonte:** [Subagents](https://kiro.dev/docs/chat/subagents/)

#### Subagents Built-in

O Kiro possui dois subagents built-in:
- **Context gathering** — explora o projeto e coleta contexto relevante
- **General purpose** — usado para paralelizar tarefas genéricas

#### Comportamento

- Subagents rodam em paralelo, cada um com sua própria janela de contexto
- O agente principal espera todos os subagents terminarem antes de continuar
- Resultados são retornados automaticamente ao agente principal
- Steering files e MCP servers funcionam nos subagents igual ao agente principal
- Subagents NÃO têm acesso a Specs
- Hooks NÃO disparam dentro de subagents

#### Custom Subagents

Você pode definir custom agents criando um arquivo markdown (.md) em `~/.kiro/agents` (global) ou `.kiro/agents` (workspace). O frontmatter YAML define os atributos e o corpo markdown é o system prompt.

Exemplo:
```markdown
# ~/.kiro/agents/code-reviewer.md
---
name: code-reviewer
description: Expert code review assistant.
tools: ["read", "@context7"]
model: claude-sonnet-4
---

You are a senior code reviewer.

## Your Responsibilities
- Review code for correctness, performance, and security
```

**Atributos do frontmatter:**

| Atributo | Descrição | Default se omitido |
|----------|-----------|-------------------|
| name | Nome do agente (obrigatório) | Nome do arquivo .md |
| description | Descrição do agente | Sem descrição |
| tools | Lista de ferramentas disponíveis | Nenhuma |
| model | Modelo a usar | Modelo selecionado no chat |
| includeMcpJson | Incluir todas as ferramentas MCP | false |
| includePowers | Incluir ferramentas MCP dos Powers | false |

**Valores possíveis no campo tools:**
- `read`, `write`, `shell`, `web`, `spec` — categorias de ferramentas built-in
- `@builtin` — todas as ferramentas built-in
- `@<mcp_server>` — todas as ferramentas de um MCP server (ex: `@figma`)
- `@<mcp_server>/<tool>` — ferramenta específica (ex: `@figma/get_figjam`)
- `"*"` — wildcard, inclui tudo

**Invocação:**
- Automática: Kiro seleciona baseado na description
- Explícita: "Use o code-reviewer subagent para revisar meu código"
- Slash command: `/code-reviewer encontre problemas de performance`

**Fonte:** [Custom Subagents](https://kiro.dev/docs/chat/subagents/#custom-subagents)

### 4.8 Dev Servers (IDE)

O Kiro IDE pode gerenciar processos de longa duração (dev servers, build watchers, test runners) diretamente do chat, eliminando a necessidade de alternar entre terminal e IDE.

**Fonte:** [Dev Servers](https://kiro.dev/docs/chat/dev-servers/)

#### Como funciona

Quando você pede ao Kiro para rodar um comando de longa duração, ele automaticamente:
- Cria um terminal dedicado com nome descritivo (ex: "Kiro: npm run dev")
- Inicia o processo em background
- Devolve o controle imediatamente para você continuar trabalhando
- Rastreia o processo para consulta de status ou output a qualquer momento

#### Uso

- Iniciar: "Inicie o servidor de desenvolvimento" ou "Rode npm run watch"
- Monitorar: "Verifique o output do dev server" ou "Tem algum erro no build?"
- Listar: "Quais processos estão rodando?"
- Parar: "Pare o dev server" ou "Termine o npm run watch"

#### Reuso de processos

Se você pedir para iniciar um processo que já está rodando (mesmo comando, mesmo diretório), o Kiro reutiliza o processo existente ao invés de criar duplicata.

### 4.9 Custom Agents (CLI)

Custom agents no Kiro CLI permitem personalizar o comportamento do agente para tarefas específicas, definindo quais ferramentas estão disponíveis, quais permissões são concedidas e qual contexto é incluído automaticamente.

Cada custom agent é definido por um arquivo de configuração que especifica:
- **prompt** — contexto de alto nível para o agente
- **mcpServers** — servidores MCP que o agente pode acessar
- **tools** — ferramentas disponíveis para o agente
- **toolAliases** — remapeamento de nomes de ferramentas para lidar com colisões
- **allowedTools** — ferramentas que podem ser usadas sem solicitar aprovação

**Criação simplificada:** O comando `/agent create` usa modo assistido por IA por padrão — descreva o que quer e o Kiro gera a configuração. Use `--manual` para o fluxo anterior baseado em editor.

#### Auto Agent

O Kiro CLI inclui um Auto Agent que escolhe dinamicamente o modelo otimal para cada interação, balanceando performance, eficiência e qualidade.

#### Knowledge Bases

O Kiro CLI suporta Knowledge Bases para busca semântica em codebases grandes, com auto-indexing e configuração via schema de agente.

#### Funcionalidades Adicionais do CLI

- **Indicadores visuais de uso de contexto** — o comando `/context` mostra quanto da janela de contexto está sendo utilizado
- **Suporte a input multimodal** — o CLI aceita imagens como input
- **Créditos em tempo real** — o consumo de créditos é exibido em tempo real
- **File references** — sintaxe `@path` para incluir conteúdo de arquivos inline (ex: `@src/main.rs`)
- **Session settings tool** — ajuste configurações temporariamente dentro da sessão atual sem modificar arquivos de config
- **Granular tool trust** — ao aprovar ferramentas, escolha escopos de confiança (comando exato, comando com argumentos, wildcards)
- **Help Agent** — agente built-in para respostas sobre o CLI via `/help`
- **Multi-session support** — trabalhe com múltiplas sessões de chat via `/chat resume`
- **Grep e Glob tools** — ferramentas built-in para busca rápida de conteúdo e arquivos

**Fontes:**
- [Custom Agents](https://kiro.dev/docs/cli/custom-agents/)
- [Creating Custom Agents](https://kiro.dev/docs/cli/custom-agents/creating/)
- [Agent Configuration Reference](https://kiro.dev/docs/cli/custom-agents/configuration-reference/)

### 4.10 Plan Agent (CLI)

O Plan agent é um agente built-in especializado que ajuda a transformar ideias em planos de implementação estruturados.

- Acessível via `Shift + Tab` ou o comando `/plan`
- Opera em modo read-only — pode explorar o codebase mas não pode modificar arquivos

**Workflow:**
1. **Requirements gathering** — perguntas estruturadas com opções de múltipla escolha para refinar a ideia
2. **Research & analysis** — explora o codebase usando code intelligence, grep e glob tools
3. **Implementation plan** — cria breakdowns detalhados de tarefas com objetivos claros
4. **Handoff** — transfere o plano aprovado para o agente de execução

**Fonte:** [Plan Agent](https://kiro.dev/docs/cli/chat/planning-agent/)

### 4.11 Agent Client Protocol — ACP (CLI)

O Kiro CLI implementa o Agent Client Protocol (ACP), um padrão aberto que permite que agentes de IA trabalhem com qualquer editor compatível.

Para iniciar o Kiro como agente ACP:
```
kiro-cli acp
```

O Kiro inicia como um agente compatível com ACP que se comunica via stdin/stdout usando JSON-RPC. Suporta métodos ACP padrão além de extensões para slash commands, ferramentas MCP e gerenciamento de sessão.

**Editores compatíveis com ACP:**
- JetBrains IDEs (IntelliJ, WebStorm, PyCharm, etc.)
- Zed
- Eclipse
- Emacs
- Neovim
- Toad
- E outros editores compatíveis com ACP

O ACP funciona de forma análoga ao Language Server Protocol (LSP), mas para agentes de IA.

**Fonte:** [Agent Client Protocol (ACP)](https://kiro.dev/docs/cli/acp/)

### 4.12 Terminal UI (CLI)

Desde a versão 2.0 (abril/2026), a Terminal UI é a **interface padrão** do Kiro CLI, promovida de experimental. Ela oferece renderização rica de markdown com realce de sintaxe, painéis de sobreposição interativos, progresso visual das ferramentas e um conjunto completo de atalhos de teclado.

**Fonte:** [Terminal UI](https://kiro.dev/docs/cli/terminal-ui/) | [Comparativo Terminal UI vs Clássica](https://kiro.dev/docs/cli/terminal-ui/comparison/)

#### Principais Recursos

- **Renderização**: código com realce, tabelas, listas, citações e formatação aninhada; atualizações sem flicker em terminais com saída sincronizada
- **Exibição de ferramentas**: cada ferramenta tem componente visual dedicado com ícones de status (✓ sucesso, ✗ erro, ⏸ aguardando aprovação), saída recolhível (`Ctrl+O`) e barras de progresso para operações MCP longas
- **Streaming de saída shell em tempo real** (CLI 2.1): comandos shell têm saída streamada linha a linha, útil para builds, testes e deploys
- **Escape para shell**: prefixar `!` executa um comando shell sem passar pelo agente
- **Entrada avançada**: nova linha com `Shift+Enter`, `Ctrl+J` ou `Alt+Enter`; referência a arquivos com `@path` e tab-complete; fila de mensagens enquanto o agente processa; histórico persistente; busca reversa com `Ctrl+R`; editor multilinha via `/editor`
- **Painéis de sobreposição**: `/help`, `/context`, `/tools`, `/mcp`, `/knowledge`, `/code` abrem painéis pesquisáveis
- **Activity tray** (`Ctrl+X`): progresso e mensagens em fila
- **Crew monitor** (`Ctrl+G`): visualização em tempo real de subagentes em fluxos multi-agente
- **Temas** (3 nativos: dark, light, safe ANSI) com autodetecção e personalização via `/theme`
- **Links markdown clicáveis** em iTerm2, WezTerm, kitty e Ghostty
- **Suporte a CJK, emoji e caracteres acentuados**
- **Plataformas suportadas**: macOS, Linux (incluindo RHEL) e Windows

#### Slash Commands da Terminal UI

`/help`, `/context`, `/usage`, `/knowledge`, `/prompts`, `/editor`, `/feedback`, `/paste`, `/chat`, `/plan`, `/agent`, `/model`, `/mcp`, `/tools`, `/code`, `/hooks`, `/guide`, `/transcript`, `/theme`, `/copy`, `/spawn`, `/clear`, `/compact`, `/reply`, `/exit`, `/<skill-name>`.

#### Comandos Úteis

```bash
# Iniciar sessão (Terminal UI é o padrão)
kiro-cli chat

# Retomar sessão específica
kiro-cli chat --resume-id <SESSION_ID>

# Usar a interface clássica em uma sessão
kiro-cli --classic

# Alternar para clássica permanentemente
kiro-cli settings chat.ui "classic"

# Desabilitar recursos específicos
KIRO_NO_HYPERLINKS=1 kiro-cli chat
KIRO_NO_PROGRESS=1 kiro-cli chat
```

#### Limitações Conhecidas

- Comandos shell interativos como `rm -i`, `sudo`, `npm init`, prompts de SSH **não são suportados** — use alternativas não interativas (`npm init -y`, `rm` sem `-i`)
- Ferramentas de diff externas (setting `chat.diffTool`) ainda não são suportadas — o diff viewer embutido é utilizado
- `/tangent`, modo Vi de edição, `/changelog`, `/logdump` e `/experiment` ainda não foram portados
- Atalhos de edição estilo Emacs: `Ctrl+W` (apagar palavra), `Ctrl+K` (kill até fim da linha), `Ctrl+U` (kill até início), `Ctrl+Y` (yank), `Ctrl+_` (undo)

#### Comparativo com a Interface Clássica

| Recurso | Clássica | Terminal UI |
|---------|----------|-------------|
| Saída de ferramenta shell | Streaming em tempo real | Streaming em tempo real (desde CLI 2.1) |
| Comandos interativos | `rm -i`, `sudo`, prompts de `ssh` funcionam | Não suportados |
| `/help` | Inicia agente de ajuda para Q&A | Abre painel pesquisável de comandos |
| Fluxo de aprovação | Menu y/n/t em texto | Barra de notificação com drill-in |
| Indicadores do prompt | Perfil, % de contexto | Chip de agente, chip de modelo, % contexto, branch git, cwd |

**Knowledge Management experimental:** Knowledge Bases com auto-indexing para busca semântica também estão disponíveis. Funcionalidades experimentais podem ser ativadas/desativadas via `/experiment`.

### 4.13 MCP (Model Context Protocol)

O Kiro suporta servidores MCP para conectar ferramentas e fontes de dados externas. A configuração é feita via arquivos `mcp.json`:

- Configuração por workspace: `.kiro/settings/mcp.json`
- Configuração global (usuário): `~/.kiro/settings/mcp.json`

#### Remote MCP

O Kiro oferece suporte nativo a servidores MCP remotos via protocolo Streamable HTTP, permitindo conectar-se a servidores MCP hospedados na nuvem sem necessidade de processos locais.

**Características do Remote MCP:**
- **Streamable HTTP** — protocolo de transporte para comunicação com servidores MCP remotos
- **Dynamic client registration** — autenticação automática com servidores remotos
- **Variáveis de ambiente** — suporte a sintaxe `${ENV_VAR}` nos arquivos de configuração MCP
- **Botão "Add to Kiro"** — instalação com um clique de servidores MCP a partir de páginas web
- **MCP Prompts e Resource Templates** — servidores MCP podem fornecer prompts e templates de recursos que aparecem no menu de contexto (#) no chat
- **Elicitation** — durante execução de ferramentas, servidores podem solicitar input adicional do usuário

#### Server Directory (Diretório de Servidores)

O Kiro mantém um diretório curado de servidores MCP com instalação em um clique ("Add to Kiro"). Servidores disponíveis incluem:

| Servidor | Descrição |
|----------|-----------|
| Amazon Devices Builder Tools | Desenvolver, testar e debugar apps para dispositivos Amazon |
| Amplitude | Dados de produto, experimentos e comportamento de usuário |
| AWS Documentation | Acesso à documentação AWS com busca e recomendações |
| Azure | Interagir com serviços e recursos Azure |
| Chrome DevTools | Controlar e inspecionar Chrome para automação e debugging |
| Context7 | Documentação atualizada de código para qualquer biblioteca |
| Datadog | Plataforma de observabilidade e segurança |
| Docker | Gerenciar containers e imagens Docker |
| Dynatrace | Plataforma de observabilidade |
| Elastic | Interface para Elasticsearch, AI, Observability e Security |
| Filesystem | Operações seguras de arquivo em diretórios permitidos |
| GCP | Gerenciar recursos Google Cloud Platform |
| Git | Ler, buscar e manipular repositórios Git |
| GitHub | Interagir com repositórios, issues e pull requests |
| GitLab | Gerenciar issues, merge requests e pipelines |
| Kubernetes | Interagir com clusters Kubernetes |
| Memory | Sistema de memória persistente baseado em knowledge graph |
| MongoDB | Interagir com bancos de dados MongoDB |
| Neo4j | Interagir com bancos de dados de grafos Neo4j |
| New Relic | Monitorar e analisar performance de aplicações |
| Pinecone | Banco de dados vetorial para busca semântica e RAG |
| Playwright | Automação de browser para web scraping e testes |
| PostgreSQL | Consultar e gerenciar bancos de dados PostgreSQL |
| Postman | Interagir com coleções, APIs e ambientes Postman |
| Sequential Thinking | Resolução de problemas dinâmica e reflexiva |
| Strands Agent | Documentação sobre Strands Agents |
| Web Search | Buscar na web usando Brave Search API |

#### Tool Search (CLI 2.1+)

O Tool Search carrega ferramentas MCP **sob demanda** em vez de enviar todas as definições a cada requisição. Isso mantém a janela de contexto livre quando há muitos servidores MCP configurados e permite que o agente descubra automaticamente a ferramenta correta.

**Quando habilitar:**
- 5 ou mais servidores MCP configurados
- Estouros de janela de contexto em conversas longas
- `/tools` mostra que ferramentas MCP consomem mais de 50.000 tokens no total

**Configurações:**

| Setting | Padrão | Função |
|---------|--------|--------|
| `toolSearch.enabled` | `false` | Interruptor principal |
| `toolSearch.minPct` | `5` | Ativa quando specs MCP excedem esse % do contexto |
| `toolSearch.minTokens` | `50000` | Ativa quando specs MCP excedem essa contagem de tokens |

Com ambos os thresholds definidos, a ativação ocorre por OR (qualquer um atingido). Ambos em `0` mantêm o Tool Search sempre ativo.

**Habilitar:**
```bash
kiro-cli settings toolSearch.enabled true
```

**Como funciona:**
1. **Indexação**: ao conectar, servidores MCP têm todas as specs indexadas por nome, servidor, descrição e parâmetros
2. **Lista diferida**: em vez de schemas JSON completos, o modelo recebe uma lista compacta `server_name::tool_name: description` (descrições truncadas em 1KB)
3. **Carregamento sob demanda**: o modelo chama `tool_search` com `tool_id` exato (ex.: `builder-mcp::InternalSearch`) ou `query` por palavra-chave
4. **Ativação**: ferramentas encontradas são carregadas com schemas completos nas requisições seguintes

**Fonte:** [Tool Search](https://kiro.dev/docs/cli/mcp/tool-search/)

#### Compartilhando seu MCP Server

Crie links de instalação com um clique para seu servidor MCP:

```
https://kiro.dev/launch/mcp/add?name=<server-name>&config=<url-encoded-config>
```

Badge "Add to Kiro" disponível em SVG para inclusão em READMEs e documentação:
```markdown
[![Add to Kiro](https://kiro.dev/images/add-to-kiro.svg)](https://kiro.dev/launch/mcp/add?name=my-server&config=...)
```

**Fonte:** [MCP Configuration](https://kiro.dev/docs/mcp/configuration/) | [Server Directory](https://kiro.dev/docs/mcp/servers/) | [MCP Security](https://kiro.dev/docs/mcp/security/)

### 4.14 Checkpointing (Pontos de Restauração)

O Kiro cria pontos de restauração automáticos durante sessões de desenvolvimento, permitindo reverter alterações feitas pelo agente a qualquer ponto da sessão.

**Características:**
- **Automático** — checkpoints são criados automaticamente conforme o agente faz alterações
- **Reversão granular** — é possível reverter a qualquer ponto da sessão, não apenas ao estado anterior
- **Preservação de histórico** — ao restaurar um checkpoint, o histórico de conversa é preservado
- **Escopo limitado** — apenas arquivos modificados pelo Kiro na sessão atual são revertidos
- **Complementar ao Git** — checkpointing complementa (não substitui) o controle de versão

**Fonte:** [Checkpointing](https://kiro.dev/docs/chat/checkpoints/) | [Kiro Changelog](https://kiro.dev/changelog/)

### 4.15 Multi-root Workspaces

O Kiro suporta múltiplas pastas de projeto em uma única janela do IDE, permitindo trabalhar com monorepos, projetos relacionados ou microsserviços lado a lado.

**Comportamento com múltiplas raízes:**
- **Specs** — aparecem em uma lista unificada com indicação clara de qual raiz de projeto cada spec pertence
- **Hooks** — são escopados à sua raiz de projeto
- **MCP configs** — configurações de todas as raízes são mescladas, com a última pasta adicionada tendo precedência
- **#codebase** — a busca abrange todas as raízes do workspace

**Fonte:** [Multi-root Workspaces](https://kiro.dev/docs/editor/multi-root-workspaces/) | [Kiro Changelog](https://kiro.dev/changelog/)

### 4.16 AST-based Code Navigation and Editing

O Kiro utiliza uma engine baseada em Abstract Syntax Tree (AST) para navegação e edição de código, proporcionando operações mais precisas e eficientes.

**Impacto:** Redução de 20% no uso de tokens medida no benchmark SWE-PolyBench.

**readCode — Navegação inteligente:**
- Para arquivos pequenos, retorna o conteúdo completo
- Para arquivos grandes, retorna signatures e estrutura (classes, funções, métodos)
- Suporta busca fuzzy por símbolos (ex: `ClassName.methodName`)

**editCode — Edição baseada em selectors:**
- Utiliza selectors tipados como `ClassName`, `functionName`, `ClassName.methodName`
- Operações tipadas: `insert_node`, `replace_node`, `delete_node`
- Resiliente a mudanças de formatação
- Fallback para edição textual quando AST não é aplicável

**Suporte a linguagens:** 18 linguagens built-in incluindo TypeScript, JavaScript, Python, Java, Go, Rust, C, C++, C#, Ruby, PHP, Swift, Kotlin, Scala, Bash, Elixir, Lua, TSX, entre outras.

**CLI — Pattern Tools:** O CLI inclui ferramentas `pattern-search` e `pattern-rewrite` que permitem encontrar e transformar código usando padrões de syntax-tree ao invés de regex textual, evitando falsos matches em string literals ou comentários.

**Fonte:** [Blog: AST-based Code Navigation](https://kiro.dev/blog/surgical-precision-with-ast/) | [Kiro Changelog](https://kiro.dev/changelog/)

### 4.17 IDE Diagnostics Integration

O agente do Kiro tem acesso direto aos diagnósticos do IDE, incluindo erros de compilação, warnings, linting e type checking, sem necessidade de executar comandos de build.

**Performance:**
- Validação em menos de **35ms** vs segundos para executar build commands
- Redução de **29%** em execuções de comandos shell durante sessões agentic

**Linguagens e ferramentas suportadas:**
- TypeScript, Python, Rust, SQL, YAML, GraphQL, Terraform, e mais
- Funciona com qualquer Language Server instalado no IDE

**Tipos de erros detectados:**
- Erros de tipo (type mismatches)
- Imports faltantes ou incorretos
- Hallucinations de propriedades
- Variáveis não utilizadas
- Erros de sintaxe
- Violações de linting

**Fonte:** [Blog: IDE Diagnostics](https://kiro.dev/blog/) | [Kiro Changelog](https://kiro.dev/changelog/)

### 4.18 Semantic Rename e Smart Relocate

O Kiro oferece ferramentas de refatoração que utilizam a API do IDE para operações precisas e seguras.

#### semanticRename
Renomeia símbolos (variáveis, funções, classes, interfaces, etc.) usando a API de renomeação do IDE, equivalente ao atalho F2. Todas as referências são atualizadas automaticamente em todo o codebase.

#### smartRelocate
Move ou renomeia arquivos atualizando automaticamente todos os imports e referências em outros arquivos.

**Linguagens suportadas:** TypeScript, JavaScript, Python, Go, Java e mais — funciona com qualquer linguagem que tenha suporte a LSP no IDE.

**Fonte:** [Blog: Semantic Rename e Smart Relocate](https://kiro.dev/blog/) | [Kiro Changelog](https://kiro.dev/changelog/)

### 4.19 Conversation Compaction (CLI)

O Kiro CLI oferece compactação de conversas para gerenciar o uso da janela de contexto em sessões longas.

**Comando `/compact`:** Libera espaço de contexto compactando o histórico da conversa atual.

**Compactação automática:** Quando a janela de contexto transborda, o Kiro CLI compacta automaticamente.

**Configuração:**
- `compaction.excludeMessages` — número de mensagens recentes a preservar sem compactação
- `compaction.excludeContextWindowPercent` — percentual da janela de contexto a manter

**Comportamento:** A compactação cria uma nova sessão internamente. A sessão original permanece acessível via `/chat resume`.

**Fonte:** [Kiro CLI Docs](https://kiro.dev/docs/cli/) | [Kiro Changelog](https://kiro.dev/changelog/)

### 4.20 Custom Extension Registry

Por padrão, o Kiro usa o marketplace de extensões em [open-vsx.org](https://open-vsx.org/). Organizações podem configurar o Kiro para usar um registry privado com um conjunto limitado de extensões aprovadas.

**Configuração:**

Localize o arquivo `product.json` no disco:
- **macOS:** `/Applications/Kiro.app/Contents/Resources/app/product.json`
- **Windows:** `C:\Program Files\Kiro\resources\app\product.json`
- **Linux:** `/usr/lib/code/product.json`

Atualize a propriedade `extensionsGallery` para apontar para seu registry privado:

```json
"extensionsGallery": {
    "serviceUrl": "https://registry.example.com/vscode/gallery",
    "itemUrl": "https://registry.example.com/vscode/item",
    "resourceUrlTemplate": "https://registry.example.com/vscode/unpkg/{publisher}/{name}/{version}/{path}",
    "controlUrl": "",
    "recommendationsUrl": "",
    "nlsBaseUrl": "",
    "publisherUrl": ""
}
```

Para configurar todas as instalações do Kiro na organização, use uma solução de MDM (Mobile Device Management) ou endpoint management para aplicar a atualização no `product.json` em todos os dispositivos.

**Fonte:** [Custom Extension Registry](https://kiro.dev/docs/editor/extension-registry/)

### 4.21 Document Attachments

O Kiro IDE permite anexar documentos diretamente a mensagens de chat, colando ou arrastando arquivos para o input.

**Formatos suportados:** PDF, CSV, DOC, DOCX, XLS, XLSX, HTML, TXT e Markdown.

**Comportamento:** Documentos são enviados ao modelo como blocos nativos de documento, permitindo que o agente leia e raciocine sobre o conteúdo. É possível anexar até 5 documentos por mensagem e misturá-los com texto e imagens no mesmo prompt.

**Fonte:** [Kiro Changelog v0.11](https://kiro.dev/changelog/ide/0-11/)

### 4.22 Hunk-Based Review (Supervised Mode)

O modo Supervised agora apresenta mudanças de arquivo como hunks individuais ao invés de diffs de arquivo completo. Cada hunk é um grupo lógico de linhas relacionadas que pode ser independentemente aceito, rejeitado ou discutido com chat inline.

**Opções de revisão:**
- Aceitar/rejeitar hunks individuais
- Aceitar mudanças no nível de arquivo
- Aceitar todas as mudanças de uma vez
- Discutir hunks específicos com chat inline

Funciona tanto em sessões de vibe chat quanto de spec chat.

**Fonte:** [Supervised Mode](https://kiro.dev/docs/chat/autopilot/) | [Kiro Changelog v0.10](https://kiro.dev/changelog/ide/0-10/)

### 4.23 Summarization (Sumarização de Conversas)

O Kiro IDE oferece sumarização automática de conversas para gerenciar conversas longas. Quando a conversa atinge 80% do limite da janela de contexto do modelo, o Kiro automaticamente sumariza mensagens anteriores para reduzir o uso de contexto abaixo do limite.

Um medidor de uso de contexto no painel de chat mostra qual percentual do contexto do modelo está sendo utilizado.

**Fonte:** [Summarization](https://kiro.dev/docs/chat/summarization/) | [Kiro Changelog v0.7](https://kiro.dev/changelog/ide/0-7/)

### 4.24 Slash Commands

Slash commands fornecem acesso rápido a hooks e steering files diretamente do input do chat. Digite `/` para ver comandos disponíveis e executá-los instantaneamente. Hooks com triggers manuais e steering files configurados com inclusão manual aparecem no menu de slash commands.

**Fonte:** [Slash Commands](https://kiro.dev/docs/chat/slash-commands/) | [Kiro Changelog v0.7](https://kiro.dev/changelog/ide/0-7/)

### 4.25 Headless Mode (CLI)

Desde a versão 2.0, o Kiro CLI suporta execução não interativa em pipelines CI/CD, scripts de automação e ambientes sem navegador. A autenticação é feita via API key e o prompt é passado como argumento para execução ponta a ponta.

**Principais flags:**
- `--no-interactive` — execução sem interação do usuário
- `--trust-all-tools` — confia em todas as ferramentas antecipadamente
- `--trust-tools=<categorias>` — confia apenas em categorias específicas (ex.: `read,grep,fs_write`)
- `--require-mcp-startup` — falha rapidamente caso servidores MCP não consigam conectar

**Disponibilidade:** assinantes Pro, Pro+ e Power. Em contas gerenciadas por administradores, é necessário habilitar a geração de API keys via governança enterprise.

**Exemplo básico:**

```bash
# Execução com API key + prompt
export KIRO_API_KEY=ksk_xxxxxxxx
kiro-cli chat --no-interactive "Escreva testes para o módulo auth e execute"

# Confiar apenas em categorias específicas
kiro-cli chat --no-interactive --trust-tools=read,grep "Encontre todos os comentários TODO em src/"

# Analisar um erro de build via stdin
cat build-error.log | kiro-cli chat --no-interactive "Explique esta falha de build e sugira uma correção"
```

**Exemplo GitHub Actions:**

```yaml
name: Kiro Code Review
on: [pull_request]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install Kiro CLI
        run: curl -fsSL https://cli.kiro.dev/install | bash
      - name: Review PR changes
        env:
          KIRO_API_KEY: ${{ secrets.KIRO_API_KEY }}
        run: kiro-cli chat --no-interactive --trust-tools=read,grep "Revise as mudanças deste PR em busca de problemas de segurança"
```

**Limitações:**
- Exige um prompt inicial como argumento; não permite entrada mid-session
- Slash commands interativos (`/model`, `/agent`, etc.) não estão disponíveis
- Recursos da Terminal UI são desativados

**Boas práticas:**
- Armazene `KIRO_API_KEY` como secret
- Use `--trust-tools` com categorias específicas (princípio do menor privilégio)
- Rotacione as chaves regularmente e revogue as inativas em [app.kiro.dev](https://app.kiro.dev/)

**Fonte:** [Headless Mode](https://kiro.dev/docs/cli/headless/) | [Changelog CLI 2.0](https://kiro.dev/changelog/cli/2-0/)

### 4.26 Skills como Slash Commands (CLI)

Desde a versão 2.1, skills definidas em `.kiro/skills/` (workspace) ou `~/.kiro/skills/` (global) ficam disponíveis como **slash commands** `/<nome-da-skill>`. Digitar `/` seguido do nome invoca a skill diretamente, sem precisar trocar de agente ou colar instruções no prompt.

**Localizações:**
- `.kiro/skills/` (workspace) — fluxos específicos do projeto ou convenções de equipe
- `~/.kiro/skills/` (global) — fluxos pessoais em todos os projetos
- Em caso de conflito de nomes, workspace tem prioridade sobre global

**Ativação automática:** o Kiro também avalia o pedido contra a descrição das skills e carrega a relevante automaticamente, sem precisar de slash command.

**Exemplo de uso:**

```bash
# Via linguagem natural
> Revise este PR em busca de problemas de segurança
# Kiro detecta a skill pr-review e a aplica

# Via slash command
> /pr-review

# Listar skills carregadas
> /context show
```

**Configuração em agentes customizados:** adicione URIs `skill://` ao campo `resources`:

```json
{
  "name": "my-agent",
  "resources": [
    "skill://.kiro/skills/*/SKILL.md",
    "skill://~/.kiro/skills/*/SKILL.md"
  ]
}
```

**Fonte:** [Skills no CLI](https://kiro.dev/docs/cli/skills/) | [Changelog CLI 2.1](https://kiro.dev/changelog/cli/2-1/)

### 4.27 Adaptive Thinking

Adaptive Thinking é uma capacidade que **escala automaticamente o raciocínio interno do modelo com base na complexidade da tarefa**. Perguntas simples recebem respostas rápidas; problemas arquiteturais complexos recebem análise profunda, **sem nenhuma configuração do usuário**.

**No modelo:** o Adaptive Thinking é exclusivo do **Claude Opus 4.7** (lançado em abril/2026), que leva mais tempo e produz respostas mais completas em tarefas difíceis. É diferente do planejamento e auto-correção gerais que todos os modelos Opus fazem bem.

**No CLI 2.2 (27 de abril de 2026):** o raciocínio do modelo passa a **persistir entre turnos** de uma mesma conversa. O conteúdo de pensamento de turnos anteriores continua disponível em turnos seguintes, mantendo as respostas de acompanhamento alinhadas com o raciocínio que produziu as respostas anteriores. Resultado: fluxos multi-etapa mais coerentes sem necessidade de reexplicar contexto.

**Requisitos para performance ótima:**
- Kiro IDE 0.11.133 ou superior
- Kiro CLI 2.2.0 ou superior

**Fonte:** [Models — Claude Opus 4.7](https://kiro.dev/docs/models/) | [Changelog: Opus 4.7 with Adaptive Thinking](https://kiro.dev/changelog/models/claude-opus-4-7-with-adaptive-thinking-now-available/) | [Changelog CLI 2.2](https://kiro.dev/changelog/cli/2-2/)

### 4.28 Kiro Web (Preview)

O **Kiro Web** é um agente de desenvolvimento baseado em navegador, acessível em [app.kiro.dev](https://app.kiro.dev/), que permite construir software por meio de conversas naturais. Diferente do Kiro IDE (instalado localmente) e do Kiro CLI (executado em terminal), o Kiro Web opera **inteiramente na nuvem**, clonando seus repositórios em sandbox isolado e entregando o resultado como pull requests no GitHub, sem exigir configuração local.

**Status:** Preview, disponível apenas para assinantes **Kiro Pro, Pro+ e Power**, e apenas na região **US East (N. Virginia) `us-east-1`** durante este período.

**Fonte:** [Kiro Web](https://kiro.dev/docs/web/) | [Changelog: Kiro Web Preview](https://kiro.dev/changelog/web/introducing-kiro-web-preview/)

#### 4.28.1 Pré-requisitos e Setup

**Pré-requisitos:**
- Assinatura paga do Kiro (Pro ou superior — o plano gratuito não tem acesso)
- Conta GitHub conectada ao Kiro
- Para organizações com AWS Identity Center: ativação prévia pelo administrador

**Setup com login social (AWS Builder ID):**
1. Acesse [app.kiro.dev](https://app.kiro.dev/) e faça login com seu AWS Builder ID
2. Confirme assinatura Pro ou superior
3. Conecte sua conta GitHub

**Setup com AWS Identity Center:**
1. O administrador ativa o Kiro Web em **Settings > Kiro Settings > Autonomous agents** na conta AWS onde o Kiro está configurado
2. O usuário faz login em [app.kiro.dev](https://app.kiro.dev/) com credenciais do Identity Center
3. O Kiro Web exige um **Kiro Profile** — não funciona com Q Developer Profiles
4. Conecte a conta GitHub

**Conectar GitHub:**
1. Em **Settings > Agent**, clique em **Connect GitHub**
2. Autorize o **Kiro Agent GitHub app**
3. Selecione os repositórios disponíveis ao agente

São necessárias permissões de **escrita** (write) nos repositórios para que o agente crie branches e abra pull requests.

**Fonte:** [Web Setup](https://kiro.dev/docs/web/setup/) | [Identity Center Setup](https://kiro.dev/docs/web/identity-center/)

#### 4.28.2 Modos: Colaborativo vs Autônomo

O Kiro Web oferece dois modos complementares, alternáveis pelo toggle **Autonomous** na barra de entrada antes de enviar a mensagem.

**Modo Colaborativo (padrão)** — você conduz a conversa e itera junto com o agente. Ideal para trabalho exploratório, discussão de design e decisões arquiteturais.

Fluxo típico:
1. Em [app.kiro.dev](https://app.kiro.dev/), clique em **New session**
2. Selecione um ou mais repositórios em **Select repo**
3. Descreva o que deseja construir
4. Discuta abordagens e implementações
5. Peça ao agente para abrir um pull request quando estiver satisfeito

Recursos: busca web em tempo real (com citações registradas), contexto completo dos repositórios selecionados, aprendizados incorporados de revisões anteriores, trabalho coordenado em múltiplos repositórios na mesma sessão, thread única por sessão.

**Modo Autônomo** — o agente assume a responsabilidade do resultado ponta a ponta. O modelo é selecionado automaticamente.

Processo em 4 fases:
1. **Clarification** — o agente faz perguntas iniciais sobre requisitos, restrições e preferências
2. **Planning** — decompõe o trabalho em etapas, gera requisitos e critérios de aceitação
3. **Execution** — sub-agentes especializados executam cada etapa
4. **Completion** — abre um ou mais pull requests com descrições detalhadas

**Quando usar cada modo:**

| Modo Autônomo | Modo Colaborativo |
|---------------|-------------------|
| Features bem definidas | Trabalho exploratório |
| Bugs com passos de reprodução claros | Discussões de design |
| Escrever testes para código existente | Tarefas com iteração próxima ao agente |
| Refatorações seguindo padrões estabelecidos | Brainstorm de abordagens |
| Atualização de documentação ou configuração | — |

Se o agente precisar de esclarecimentos durante execução autônoma, a tarefa entra em **Needs attention** aguardando input.

**Stop Control (atualização de 18/mai/2026):** é possível **parar o agente no meio de uma tarefa**, ver progresso enquanto o workspace é provisionado, e o layout em telas pequenas ficou mais polido. Várias melhorias de estabilidade de sessão também foram aplicadas.

**Retenção de dados:** sessões expiram após 90 dias; mensagens e logs são excluídos. Pull requests, alterações de código e conversas no GitHub permanecem.

**Fonte:** [Using the Agent](https://kiro.dev/docs/web/using-the-agent/) | [Autonomous Mode](https://kiro.dev/docs/web/autonomous-mode/)

#### 4.28.3 Fluxo GitHub-Nativo

O Kiro Web é GitHub-nativo: o agente clona repositórios autorizados no sandbox, cria feature branches a partir da branch padrão, commits com mensagens claras (você e o agente como co-autores) e abre pull requests detalhados.

**Atribuindo tarefas a partir de Issues:**
- **Label `kiro`** na issue — o Kiro inicia o trabalho e passa a escutar todos os comentários para contexto e feedback
- **Comentário `/kiro`** — atribui aquela issue ao Kiro (o autor precisa ter conta GitHub registrada no Kiro; o Kiro Agent GitHub app precisa estar instalado no repo)

**Comandos de PR para revisão:**
- **`/kiro all`** — endereça todos os comentários de todos os revisores em todo o PR
- **`/kiro fix`** — endereça todos os comentários de uma thread de conversa específica

Para impedir que um comentário seja tratado, apague-o ou responda com sua perspectiva antes de usar o comando. Feedback de GitHub Actions (checks, testes, varreduras de segurança) é automaticamente tratado quando você fornece qualquer feedback.

**Autoria do PR:** por padrão, PRs são criados pelo Kiro Agent GitHub app. É possível alternar para que PRs sejam criados como seu usuário GitHub em **Settings > Agent > Pull request > Create pull requests as your GitHub user** — útil para repos com branch protection rules.

**Permissões exigidas (Read & Write):** Actions, Checks, Contents, Issues, Pull requests, Workflows. Read-only: Metadata (obrigatório), Administration, Commit statuses. O agente respeita branch protection rules e políticas da organização — não consegue fazer push direto em branches protegidas.

**Múltiplos usuários no mesmo repositório:** se dois usuários atribuírem a mesma issue, o Kiro cria tarefas separadas para cada um, em sandboxes independentes. Coordene para evitar retrabalho.

**Fonte:** [GitHub Integration](https://kiro.dev/docs/web/github/)

#### 4.28.4 Sandbox Isolado

Cada tarefa executa em seu próprio sandbox isolado, configurável em **Agent settings > Sandbox**.

**Ciclo de vida:**
1. Provisiona o ambiente isolado
2. Clona os repositórios autorizados
3. Configura o ambiente com base em settings detectados do projeto
4. Executa a tarefa com acesso apenas aos recursos permitidos explicitamente
5. Destrói o sandbox ao concluir

**Áreas configuráveis:** controle de acesso à internet (domínios permitidos), Powers e servidores MCP customizados, variáveis de ambiente e secrets, configuração geral do ambiente.

**Fonte:** [Sandbox](https://kiro.dev/docs/web/sandbox/)

#### 4.28.5 Steering que Atravessa Sessões

O steering dá ao agente conhecimento persistente sobre o código via arquivos markdown em `.kiro/steering/` na raiz do repositório. O agente carrega esses arquivos automaticamente no início de cada sessão, usando o **mesmo formato** do Kiro IDE e Kiro CLI.

**Usos comuns:**
- Convenções de código e style guides
- Padrões de arquitetura e decisões de design
- Preferências de stack e requisitos de versão
- Abordagens de testes e expectativas de cobertura
- Templates de descrição de PR e formato de mensagem de commit

**Formas adicionais de steering:**
- **Via revisões de PR** — comentários como "always use our standard error handling" fazem o agente aprender e aplicar esses padrões em trabalhos futuros em **todos os seus repositórios**. Apenas o feedback do usuário que criou a tarefa influencia os aprendizados
- **Durante a sessão** — oriente em tempo real no chat
- **No modo autônomo** — as respostas às perguntas de clarificação iniciais funcionam como steering

**Fonte:** [Web Steering](https://kiro.dev/docs/web/steering/)

#### 4.28.6 Limitações do Identity Center no Kiro Web (Preview)

As seguintes configurações compartilhadas **não se aplicam** ao Kiro Web:
- Include suggestions with code references
- Model Context Protocol (MCP)
- Model availability
- Member account subscriptions
- MCP registry URL
- Encryption key — **Customer Managed Keys (CMK) não são suportadas** no Kiro Web

Políticas de governança empresarial (seleção de modelos, controles de ferramentas web) também não estão disponíveis durante o Preview. As configurações do agente (conexões GitHub, sandbox, preferências de coleta de dados) são gerenciadas individualmente por cada usuário na página de Settings do Kiro Web.

> **Aviso de segurança:** selecione apenas repositórios em que você confia, especialmente ao misturar público e privado — o agente aprende e segue instruções contidas no código, mesmo que sejam maliciosas.

### 4.29 Modelos Disponíveis

O Kiro oferece uma ampla seleção de modelos de linguagem com diferentes trade-offs entre custo, contexto e capacidade. A disponibilidade pode variar entre IDE, CLI e Web, e alguns modelos estão em status Experimental.

**Fonte:** [Modelos](https://kiro.dev/docs/models/)

#### 4.29.1 Catálogo de Modelos (maio/2026)

| Modelo | Contexto | Custo (x Auto) | Regiões | Status |
|--------|----------|----------------|---------|--------|
| Claude Opus 4.7 | 1M | 2.2x | us-east-1, eu-central-1 | Experimental |
| Claude Opus 4.6 | 1M | 2.2x | us-east-1, eu-central-1 | Active |
| Claude Opus 4.5 | 200K | 2.2x | us-east-1, eu-central-1 | Active |
| Claude Sonnet 4.6 | 1M | 1.3x | us-east-1, eu-central-1 | Active |
| Claude Sonnet 4.5 | 200K | 1.3x | us-east-1, eu-central-1 | Active |
| Claude Sonnet 4.0 | 200K | 1.3x | us-east-1, eu-central-1 | Active |
| Auto | — | 1.0x | us-east-1, eu-central-1 | Active |
| Claude Haiku 4.5 | 200K | 0.4x | us-east-1, eu-central-1 | Active |
| GLM-5 | 200K | 0.5x | us-east-1 | Experimental |
| MiniMax M2.5 | 200K | 0.25x | us-east-1, eu-central-1 | Experimental |
| DeepSeek 3.2 | 128K | 0.25x | us-east-1 | Experimental |
| MiniMax M2.1 | 200K | 0.15x | us-east-1, eu-central-1 | Experimental |
| Qwen3 Coder Next | 256K | 0.05x | us-east-1, eu-central-1 | Experimental |

#### 4.29.2 Destaques

**Claude Opus 4.7 — Adaptive Thinking:**
- Modelo de codificação mais capaz da Anthropic no Kiro, upgrade direto do 4.6
- Escala automaticamente o raciocínio com base na complexidade da tarefa (exclusividade do 4.7)
- Segue instruções com mais precisão; verifica suas próprias saídas antes de reportar
- Visão 3x mais alta em resolução — útil para screenshots densos e diagramas
- Disponível para Pro, Pro+ e Power, e IAM Identity Center
- Requer IDE 0.11.133+ e CLI 2.2.0+ para performance ótima

**GLM-5 — Contexto em escala de repositório:**
- Open weight, sparse mixture-of-experts com janela de 200K
- Manutenção de coerência durante uso multi-step de ferramentas em grandes codebases
- Ideal para migrações cross-file, desenvolvimento full-stack e refactoring de legado
- Custo: 0.5x Auto, inferência em us-east-1

#### 4.29.3 Guia Rápido de Seleção

| Cenário | Modelo recomendado |
|---------|---------------------|
| Desenvolvimento geral | Auto |
| Baseline previsível | Sonnet 4.0 |
| Coding agêntico forte | Sonnet 4.5 |
| Alta inteligência eficiente | Sonnet 4.6 |
| Codebases grandes ou specs complexas | Opus 4.7 (upgrade direto do 4.6) |
| Problemas multi-sistema complexos | Opus 4.5 |
| Velocidade ou economia de créditos | Haiku 4.5 |
| Coding de custo mínimo | DeepSeek 3.2 |
| Coding frontier de baixo custo | MiniMax M2.5 |
| Trabalho agêntico em escala de repo | GLM-5 |
| Programação multilíngue | MiniMax M2.1 |
| Sessões longas de coding | Qwen3 Coder Next |

**Diferenças comportamentais:**
- **Profundidade de planejamento:** Opus planeja mais antes de agir; Sonnet e Haiku são mais diretos
- **Adaptive thinking:** exclusivo Opus 4.7, escala raciocínio automaticamente
- **Auto-correção:** todos os Opus pegam os próprios erros; Opus 4.7 vai além verificando saídas antes de reportar
- **Endurance:** Opus mantém foco melhor em sessões estendidas; Haiku e Sonnet são melhores para interações curtas e focadas
- **Iniciativa:** Opus toma mais iniciativa; Sonnet é mais conservador

### 4.30 Rewind Conversations (CLI)

Desde a versão 2.4 (maio/2026), o Kiro CLI permite voltar a qualquer prompt anterior em uma conversa e continuar a partir daquele ponto em uma nova sessão. Use `/rewind` para escolher um turno e ramificar sem perder o thread original.

**Como funciona:**
- Cria uma **nova sessão** que começa a partir do turno selecionado
- A sessão original permanece intacta — é possível retornar via `/chat resume`
- O rewind cria uma **ramificação de conversa** — não desfaz alterações de arquivo já feitas. Para reverter arquivos, use seu sistema de controle de versão

**Comandos:**

```bash
# Abrir o seletor interativo de turnos
/rewind

# Saltar diretamente para o turno 4
/rewind 4
```

O seletor mostra: preview do prompt em cada turno, percentual de uso da janela de contexto naquele ponto, e turnos listados do mais recente para o mais antigo.

**Casos de uso:**
- **Backtracking** — o agente fez uma suposição errada três turnos atrás e tudo desde então construiu sobre isso
- **Explorar alternativas** — testar uma abordagem diferente sem perder a primeira tentativa
- **Recuperar de poluição de contexto** — limpar o histórico quando muito conteúdo irrelevante se acumulou
- **A/B testing de prompts** — bifurcar no mesmo turno com instruções diferentes para comparar

**Fonte:** [Rewind](https://kiro.dev/docs/cli/chat/rewind/) | [Changelog CLI 2.4](https://kiro.dev/changelog/cli/2-4/)

### 4.31 Reasoning Effort (CLI)

O comando `/effort` controla quanto raciocínio o modelo aplica aos prompts. Níveis mais baixos produzem respostas mais rápidas e curtas; níveis mais altos consomem mais tokens em análise profunda, raciocínio multi-step e geração completa de código.

**Níveis disponíveis:**

| Nível | Quando usar |
|-------|-------------|
| `low` | Respostas rápidas e concisas. Boas para perguntas simples e consultas pontuais |
| `medium` | Raciocínio balanceado. Adequado para a maioria das tarefas de desenvolvimento |
| `high` | Análise profunda. Melhor para refactorings complexos e decisões arquiteturais |
| `xhigh` | Raciocínio estendido. Útil para mudanças multi-arquivo e problemas nuançados |
| `max` | Profundidade máxima. Melhor para debugging difícil, análise de segurança e lógica intrincada |

**Modelos suportados:**

| Modelo | Níveis disponíveis |
|--------|--------------------|
| Claude Opus 4.7 | low, medium, high, xhigh, max |
| Claude Opus 4.6 | low, medium, high, max |
| Claude Sonnet 4.6 | low, medium, high, max |

Nem todos os modelos suportam todos os níveis. O seletor mostra apenas os níveis disponíveis para o modelo atual.

**Comandos:**

```bash
# Abrir o seletor interativo
/effort

# Definir diretamente
/effort high
```

**Quando ajustar:**
- **Aumentar** quando o agente está dando respostas superficiais, perdendo edge cases ou produzindo implementações incompletas
- **Reduzir** quando você precisa de respostas rápidas e não quer esperar por raciocínio estendido
- Use `max` para revisões de segurança, sessões complexas de debugging ou quando o agente precisa considerar muitas restrições interagindo

**Fonte:** [Effort](https://kiro.dev/docs/cli/chat/effort/) | [Changelog CLI 2.4](https://kiro.dev/changelog/cli/2-4/)

### 4.32 Unified Settings Menu (CLI)

A versão 2.4 introduz `/settings` como menu unificado para personalização visual, atalhos de teclado e configuração de terminal — sem precisar sair da sessão de chat.

**Subcomandos:**

| Subcomando | Função |
|------------|--------|
| `/settings theme` | Personalizar cores do prompt e respostas (com preview ao vivo) |
| `/settings keybindings` | Visualizar atalhos de teclado (referência read-only) |
| `/settings terminal` | Habilitar `Shift+Enter` e `Option+Enter` como newline shortcuts |
| `/settings display` | Toggles visuais (animations, ASCII art, icons) |

O comando `/theme` antigo continua funcionando como atalho.

**Persistência:** mudanças são salvas em `~/.kiro/settings/cli.json` e aplicadas em sessões futuras. Edite o arquivo diretamente com `kiro-cli settings open`.

**Configuração de terminal:** `/settings terminal` aplica automaticamente bindings nos seguintes terminais:
- VS Code integrated terminal, Alacritty, Zed, Apple Terminal — auto-configurados
- iTerm2, Kitty, Ghostty, WezTerm, Warp — suporte nativo (sem configuração)

Um backup `.bak` é criado antes de qualquer alteração no arquivo de configuração do terminal.

**Para usuários de tmux**, adicione ao `tmux.conf`:
```bash
set -s extended-keys on
set -as terminal-features 'xterm*:extkeys'
```

**Alteração de keybindings:**

```bash
kiro-cli settings chat.keybindings.cancelStream "ctrl+x"
kiro-cli settings chat.keybindings.closeMenu "ctrl+["
kiro-cli settings chat.keybindings.quit "ctrl+shift+q"
```

**Fonte:** [In-session Settings](https://kiro.dev/docs/cli/chat/settings/) | [Changelog CLI 2.4](https://kiro.dev/changelog/cli/2-4/)

### 4.33 KIRO_HOME e Configurações Avançadas (CLI 2.3)

A versão 2.3 (maio/2026) trouxe quatro recursos avançados de configuração e integração para o Kiro CLI.

#### KIRO_HOME — Diretório customizado

A variável de ambiente `KIRO_HOME` redireciona o Kiro para usar um diretório diferente para agents globais, prompts, skills, steering, settings e sessions.

```bash
export KIRO_HOME=/caminho/customizado
kiro-cli chat
```

**Casos de uso:**
- Gerenciamento de dotfiles entre máquinas
- Separação entre perfis de trabalho e pessoal
- Isolamento do estado do Kiro em ambientes containerizados

#### OAuth Client ID para Servidores MCP

Permite conectar a servidores MCP HTTP que **não** suportam Dynamic Client Registration, definindo um `oauth.clientId` pré-registrado na configuração do MCP.

Isso desbloqueia serviços como **Slack, GitHub e Figma** que exigem registro manual de aplicação para OAuth, eliminando a necessidade de rodar um proxy próprio.

**Fonte:** [OAuth Configuration](https://kiro.dev/docs/cli/custom-agents/configuration-reference/#oauth-configuration)

#### V2 TUI Keybindings Configuráveis

As ações de cancel, close-menu e quit no V2 TUI agora podem ser remapeadas. Útil quando `Ctrl+C` e `Esc` conflitam com o prefix do tmux ou bindings de outros terminais.

```bash
kiro-cli settings chat.keybindings.cancelStream "ctrl+x"
kiro-cli settings chat.keybindings.closeMenu "ctrl+["
kiro-cli settings chat.keybindings.quit "ctrl+shift+q"
```

#### Agent Output Side Channels

Comandos shell executados pelo agente podem agora streamar saída por **dois canais adicionais** além do stdout:

| Variável | Função |
|----------|--------|
| `$AGENT_DISPLAY_OUT` | Mostra progresso rico na TUI sem inflar o contexto do agente |
| `$AGENT_CONTEXT_OUT` | Expõe linhas no campo `agent_notes` do resultado da ferramenta |

O stdout continua funcionando como antes. Útil para wrappers que precisam separar saída visual da saída que vai ao contexto do modelo.

**Fonte:** [Side Channels](https://kiro.dev/docs/cli/reference/built-in-tools/#side-channels-for-wrapper-scripts) | [Changelog CLI 2.3](https://kiro.dev/changelog/cli/2-3/)

---

## 5. CONFIGURAÇÃO

### 5.1 Configurações do CLI

O Kiro CLI oferece personalização através de configurações detalhadas.

**Fonte:** [CLI Settings Reference](https://kiro.dev/docs/cli/reference/settings/)

### 5.2 Configuração de Chat

O Kiro CLI permite configurar o comportamento do chat agentic, incluindo diff tools customizados (delta, difftastic, VS Code) via `chat.diffTool`.

**Fonte:** [CLI Chat Configuration](https://kiro.dev/docs/cli/chat/configuration/) | [Diff Tools](https://kiro.dev/docs/cli/chat/diff-tools/)

### 5.3 Agentes Customizados

Agentes customizados permitem personalizar o comportamento do Kiro para tarefas específicas e recorrentes.

**Fontes:**
- [Custom Agents](https://kiro.dev/docs/cli/custom-agents/)
- [Creating Custom Agents](https://kiro.dev/docs/cli/custom-agents/creating/)

### 5.4 Ferramentas Built-in

O Kiro possui ferramentas integradas para auxiliar no desenvolvimento, incluindo leitura/escrita de arquivos, busca (grep/glob), execução de comandos, navegação web, entre outras.

**Fonte:** [Built-in Tools](https://kiro.dev/docs/cli/reference/built-in-tools/)

### 5.5 Gerenciamento de Permissões de Ferramentas

O Kiro CLI permite gerenciar permissões para ferramentas com escopos granulares de confiança. Para comandos shell, escolha entre confiar no comando exato, no comando com quaisquer argumentos, ou no comando base com wildcards. Para ferramentas de leitura/escrita, escope a confiança a caminhos específicos, diretório contendo, ou a ferramenta inteira.

**Fonte:** [Managing Tool Permissions](https://kiro.dev/docs/cli/chat/permissions/)

---

## 6. ACESSO ENTERPRISE

O Kiro oferece funcionalidades enterprise para organizações que precisam gerenciar acesso, identidades e faturamento de forma centralizada.

**Fonte:** [Kiro for Enterprise](https://kiro.dev/enterprise/) | [Enterprise Docs](https://kiro.dev/docs/enterprise/getting-started/)

### 6.1 Conceitos Fundamentais

#### Perfil Kiro (Kiro Profile)

Um perfil Kiro corresponde à combinação de uma conta AWS (management ou member) e a região dessa conta. Isso significa que só é possível ter um perfil por conta AWS em uma determinada região. Os perfis são configurados através do console Kiro dentro do AWS Console.

O perfil é o elemento que conecta as identidades dos usuários com suas assinaturas e configurações do Kiro.

#### Região do Perfil

A região onde o perfil Kiro é criado determina onde os dados são armazenados e onde a inferência é realizada. Esta região pode ser diferente da região da instância do IAM Identity Center.

**Fonte:** [Enterprise Concepts](https://kiro.dev/docs/enterprise/concepts/)

### 6.2 Regiões Suportadas

O Kiro enterprise está disponível nas seguintes regiões AWS:

| Região | Código |
|--------|--------|
| US East (N. Virginia) | us-east-1 |
| Europe (Frankfurt) | eu-west-1 |
| AWS GovCloud (US-East) | us-gov-east-1 |
| AWS GovCloud (US-West) | us-gov-west-1 |

**GovCloud:** O Kiro está disponível nas regiões AWS GovCloud, permitindo que agências governamentais e contratantes usem o Kiro dentro de seus limites de compliance. A autenticação em GovCloud é feita via IAM Identity Center com Start URL GovCloud (contendo `us-gov-home`). Métodos individuais (GitHub, Google, Builder ID) não estão disponíveis em regiões GovCloud. Para clientes GovCloud, requisições de inferência são processadas usando Amazon Bedrock em AWS GovCloud (US-West).

**Fonte:** [Supported Regions](https://kiro.dev/docs/enterprise/supported-regions/) | [GovCloud Support](https://kiro.dev/changelog/general/aws-govcloud-support/)

### 6.3 Onboarding Enterprise — Quickstart

O processo de onboarding enterprise segue estes passos:

#### Passo 1: Acessar o Console Kiro na AWS
- Navegue até o console do Kiro dentro do AWS Console
- É necessário ter permissões IAM adequadas para gerenciar o Kiro

#### Passo 2: Criar um Perfil Kiro
- Use a interface disponível para criar um perfil
- O perfil conecta identidades de usuário com assinaturas e configurações
- Selecione a região desejada

#### Passo 3: Conectar um Identity Provider
- Conecte o IAM Identity Center, Okta ou Microsoft Entra ID ao perfil
- Importe usuários e grupos do seu provedor de identidade

#### Passo 4: Inscrever Usuários
- Adicione usuários ou grupos ao perfil
- Atribua os tiers de assinatura apropriados (Pro, Pro+, Power)
- Configure permissões e acessos

**Fonte:** [Onboarding Quickstart](https://kiro.dev/docs/enterprise/getting-started/)

### 6.4 Conectando um Identity Provider (IdP)

O Kiro enterprise suporta três opções de provedor de identidade para gerenciar o acesso dos usuários.

**Fonte:** [Connect an Identity Provider](https://kiro.dev/docs/enterprise/identity-provider/)

#### 6.4.1 AWS IAM Identity Center

O IAM Identity Center é a solução da AWS para conectar usuários da força de trabalho a aplicações gerenciadas pela AWS. Permite conectar um provedor de identidade existente, criar e gerenciar usuários diretamente, fornecer SSO e gerenciar acesso em múltiplas contas AWS.

**Fonte:** [Connect your IAM Identity Center](https://kiro.dev/docs/enterprise/identity-provider/iam-identity-center/)

#### 6.4.2 Okta

A configuração com Okta requer a criação de duas aplicações:
- **Aplicação OIDC** — utilizada para o login dos usuários no Kiro
- **Aplicação SAML** — utilizada para sincronização de usuários e grupos via SCIM

**Fonte:** [Connect your Okta IdP](https://kiro.dev/docs/enterprise/identity-provider/okta)

#### 6.4.3 Microsoft Entra ID (Azure AD)

Requer verificação de propriedade do domínio via registro TXT no DNS. A sincronização de usuários e grupos acontece automaticamente via SCIM.

**Fonte:** [Connect your Microsoft Entra ID IdP](https://kiro.dev/docs/enterprise/identity-provider/microsoft-entra)

### 6.5 Comparativo dos Identity Providers

| Característica | IAM Identity Center | Okta | Microsoft Entra ID |
|---------------|--------------------|----- |-------------------|
| Tipo de integração | Nativa AWS | OIDC + SAML | OIDC + SAML |
| Sincronização de usuários | Direta | SCIM automático | SCIM automático |
| Verificação de domínio | Não necessária | Necessária | Necessária (registro TXT DNS) |
| Aplicações necessárias | 1 | 2 (OIDC + SAML) | 1 |
| SSO corporativo | Sim | Sim | Sim |

### 6.6 Assinaturas Enterprise

Após conectar o IdP e importar usuários, o administrador pode atribuir assinaturas na página "Users & Groups" do console Kiro. Se um usuário estiver inscrito duas vezes no mesmo perfil (ex: em dois grupos diferentes), a cobrança será feita apenas pelo tier mais alto atribuído.

**Exportação de dados:** Administradores podem exportar dados de assinatura como CSV diretamente do console Kiro, incluindo nome do usuário, plano, status, tipo e data de ativação.

**Fonte:** [Subscribing your team](https://kiro.dev/docs/enterprise/subscribe) | [Enterprise Billing](https://kiro.dev/docs/enterprise/billing/)

### 6.7 Governança Enterprise

Administradores podem controlar quais modelos e servidores MCP estão disponíveis para seus usuários. Esses controles são gerenciados pelo console Kiro em Settings > Shared settings.

**Fonte:** [Governance](https://kiro.dev/docs/enterprise/governance/)

#### 6.7.1 Governança de Modelos

Por padrão, usuários podem acessar qualquer modelo suportado pelo Kiro. Administradores podem restringir isso ativando o gerenciamento de acesso a modelos e selecionando uma lista aprovada.

**Como configurar:**
1. Abra o console Kiro
2. Escolha Settings
3. Em Shared settings, ative "Control which models are available to users" em Model availability
4. Selecione "Manage approved list" para escolher os modelos permitidos
5. Opcionalmente, defina um modelo padrão que será aplicado automaticamente a todos os clientes

**Considerações importantes:**
- Se você gerencia a lista de modelos, novos modelos oferecidos pelo Kiro não ficam disponíveis automaticamente — é necessário adicioná-los à lista
- Você recebe uma notificação no console quando um novo modelo fica disponível
- Mudanças na lista não têm efeito imediato — clientes precisam reiniciar a sessão ou fazer logoff/login
- Especialmente relevante para requisitos de residência de dados — modelos experimentais usando inferência cross-region global podem ser removidos da lista até migrarem para GA com inferência regional

**Fonte:** [Model Governance](https://kiro.dev/docs/enterprise/governance/model/)

#### 6.7.2 Governança de MCP

Por padrão, usuários podem usar qualquer servidor MCP. Administradores podem desabilitar MCP inteiramente ou especificar uma lista de servidores MCP aprovados via MCP registry.

**Opções de controle:**
- **Toggle MCP on/off** — desabilitar MCP completamente para a organização
- **MCP Registry URL** — especificar uma URL de arquivo JSON com servidores MCP permitidos

Políticas podem ser definidas no nível da organização ou sobrescritas por conta. Exemplo: desabilitar MCP para a organização mas habilitar com allow-list para equipes específicas.

**Como configurar o MCP Registry:**
1. Crie um arquivo JSON com os servidores permitidos seguindo o formato do MCP registry standard
2. Hospede o arquivo via HTTPS (Amazon S3, Apache, nginx, etc.) com certificado SSL válido
3. No console Kiro, em Settings > Shared settings, ative MCP e insira a URL do registry

**Formato do arquivo de registry:**

O arquivo JSON suporta servidores remotos (HTTP) e locais (stdio):

```json
{
  "servers": [
    {
      "server": {
        "name": "my-remote-server",
        "title": "My server",
        "description": "My server description",
        "version": "1.0.0",
        "remotes": [
          {
            "type": "streamable-http",
            "url": "https://acme.com/my-server"
          }
        ]
      }
    },
    {
      "server": {
        "name": "my-local-server",
        "title": "My local server",
        "description": "My local server description",
        "version": "1.0.0",
        "packages": [
          {
            "registryType": "npm",
            "identifier": "@acme/my-server",
            "transport": { "type": "stdio" }
          }
        ]
      }
    }
  ]
}
```

**Registry types suportados:** `npm` (usa npx), `pypi` (usa uvx), `oci` (usa docker).

**Sincronização:** O Kiro busca o registry na inicialização e a cada 24 horas. Se um servidor local instalado não está mais no registry, o Kiro o encerra e impede reinstalação. Se a versão difere, o Kiro relança com a versão do registry.

**Parâmetros que usuários podem sobrescrever:**
- Variáveis de ambiente adicionais para servidores locais
- Headers HTTP adicionais para servidores remotos
- Timeout de requisição
- Escopo do servidor MCP (Global, Workspace, ou Agent Configuration específico)
- Permissões de confiança de ferramentas MCP

> **Aviso:** Tanto o toggle quanto as configurações de registry são aplicados no lado do cliente. Usuários finais podem potencialmente contorná-los.

**Fonte:** [MCP Governance](https://kiro.dev/docs/enterprise/governance/mcp/)

#### 6.7.3 Governança de Web Tools

Administradores usando IAM Identity Center podem controlar o acesso a ferramentas web (web search e web fetch) para sua organização, desabilitando-as em Settings > Shared settings.

**Fonte:** [Web Tools Governance](https://kiro.dev/docs/chat/webtools/)

### 6.8 Recursos Enterprise

- **Dashboard** — visão geral para usuários enterprise
- **Medição de uso** — métricas e resumos de consumo
- **Métricas de atividade por usuário** — métricas detalhadas por desenvolvedor incluindo uso de créditos, frequência de interações e adoção de funcionalidades
- **Governança** — controle centralizado de modelos, MCP e web tools
- **Exportação CSV** — download de dados de assinatura como CSV
- **Configurações** — gerenciamento de assinaturas visíveis no console
- **IAM** — controle de acesso ao console Kiro via AWS IAM

**Fontes:**
- [Enterprise Settings](https://kiro.dev/docs/enterprise/settings/)
- [Enterprise IAM](https://kiro.dev/docs/enterprise/iam/)
- [Monitor and Track](https://kiro.dev/docs/enterprise/monitor-and-track/)

---

## 7. PRIVACIDADE E SEGURANÇA

### 7.1 Visão Geral

O Kiro é uma aplicação AWS que funciona como IDE agentic standalone. A estrutura de segurança do Kiro é construída em torno da infraestrutura de segurança da AWS e segue práticas para proteger seu ambiente de desenvolvimento e dados. Segurança na nuvem é a mais alta prioridade da AWS.

**Fonte:** [Privacy and Security](https://kiro.dev/docs/privacy-and-security/)

### 7.2 Modelo de Responsabilidade Compartilhada

O modelo de responsabilidade compartilhada da AWS se aplica à proteção de dados no Kiro:

#### Segurança DA Nuvem (Responsabilidade da AWS)
- Proteção da infraestrutura global que executa os serviços AWS
- Data center e arquitetura de rede
- Conformidade com programas de auditoria de terceiros

#### Segurança NA Nuvem (Responsabilidade do Usuário)
- Controle sobre seu conteúdo hospedado na infraestrutura
- Configuração de segurança e tarefas de gerenciamento
- Sensibilidade dos dados e requisitos da empresa
- Leis e regulamentos aplicáveis

**Fonte:** [Privacy and Security](https://kiro.dev/docs/privacy-and-security/)

### 7.3 Proteção de Dados

#### Criptografia em Repouso
- O agente autônomo do Kiro criptografa dados usando chaves de criptografia AWS owned do AWS Key Management Service (AWS KMS)
- Criptografia automática e transparente

#### Criptografia em Trânsito
- Todas as transmissões de dados via HTTPS/TLS
- Requer TLS 1.2 no mínimo, recomenda TLS 1.3
- Suítes de cifra com perfect forward secrecy (PFS): DHE e ECDHE

#### Inferência Cross-Region
Para clientes GovCloud, o conteúdo permanece armazenado na região onde o perfil Kiro foi criado, com toda comunicação cross-region criptografada via TLS 1.2+.

**Fonte:** [Data Protection](https://kiro.dev/docs/privacy-and-security/data-protection/)

### 7.4 Segurança de Infraestrutura

Como serviço gerenciado, o Kiro é protegido pela segurança da rede global da AWS. O acesso ao Kiro é feito através de chamadas de API publicadas pela AWS, com TLS 1.2+ e suítes de cifra com PFS.

**Fonte:** [Infrastructure Security](https://kiro.dev/docs/privacy-and-security/infrastructure-security/)

### 7.5 Proteção de Dados do Agente Autônomo

O agente autônomo do Kiro criptografa dados usando chaves de criptografia AWS owned do AWS KMS.

**Fonte:** [Autonomous Agent Data Protection](https://kiro.dev/docs/autonomous-agent/data-protection/)

### 7.6 Segurança MCP

O Kiro implementa melhores práticas de segurança para o Model Context Protocol (MCP), incluindo orientações para configuração e uso seguro de servidores MCP, proteção de informações sensíveis e manutenção da segurança do sistema.

> **Aviso:** Servidores MCP são ferramentas de terceiros. Instale apenas servidores de fontes confiáveis e revise sua documentação e licenciamento.

**Fonte:** [MCP Security Best Practices](https://kiro.dev/docs/mcp/security/)

---

## 8. PLANOS E PREÇOS

O Kiro oferece os seguintes tiers de assinatura (valores referentes a fevereiro de 2026):

| Tier | Preço Mensal | Créditos Incluídos | Observações |
|------|-------------|-------------------|-------------|
| Free | Gratuito | 50 créditos | Tier perpétuo |
| Pro | $20/mês | Vibe + Spec requests | — |
| Pro+ | $40/mês | Maior capacidade | — |
| Power | $200/mês | Capacidade máxima | — |

- Novos usuários recebem um free trial com 500 créditos para testar funcionalidades Pro por 30 dias
- Tiers pagos incluem overages flexíveis a $0.04 por crédito adicional
- Créditos são cobrados de forma fracionada com base na complexidade do prompt (incrementos de 0.01 crédito)

### 8.1 Kiro para Estudantes

Estudantes universitários elegíveis recebem um ano completo de acesso gratuito ao Kiro com 1.000 créditos por mês. Sem necessidade de cartão de crédito ou timer de trial.

**O que está incluído:** 1.000 créditos/mês por 12 meses, com acesso completo ao Kiro IDE e CLI incluindo desenvolvimento orientado a specs.

**Como começar:**
1. Cadastre-se ou faça login em [kiro.dev/students](https://kiro.dev/students/) usando seu e-mail universitário
2. Verifique o status de estudante via SheerID (leva cerca de um minuto)
3. Comece a construir — créditos ficam disponíveis imediatamente após verificação

Disponível com 11 universidades elegíveis, com mais em breve.

**Fonte:** [Kiro for Students](https://kiro.dev/students/) | [Changelog: Kiro for Students](https://kiro.dev/changelog/general/kiro-for-students/)

### 8.2 Modelos Disponíveis

Consulte a [seção 4.29 — Modelos Disponíveis](#429-modelos-disponíveis) para o catálogo completo de modelos e multiplicadores de crédito.

Destaques:
- **Auto Agent** — balanceia automaticamente performance, eficiência e qualidade, selecionando o modelo otimal para cada interação
- **Modelos open weight** (DeepSeek, MiniMax, Qwen3 Coder Next, GLM-5) oferecem multiplicadores de crédito reduzidos (de 0.05x a 0.5x)
- **Claude Opus 4.7** (2.2x) traz Adaptive Thinking que escala o raciocínio com base na complexidade da tarefa

**Fonte:** [Pricing](https://kiro.dev/pricing/) | [Models](https://kiro.dev/docs/models/)

**Nota:** Os preços e estrutura de tiers podem ter sido atualizados. Consulte sempre a [página oficial de preços](https://kiro.dev/pricing/) para informações atuais.

**Fontes:**
- [Pricing](https://kiro.dev/pricing/)
- [Billing for Individuals](https://kiro.dev/docs/billing/)

---

## BENCHMARK: SWE-POLYBENCH

O SWE-PolyBench é o benchmark multi-linguagem criado pela Amazon para avaliar agentes de IA em tarefas de engenharia de software. É o benchmark usado pelo time do Kiro para medir melhorias como a engine AST (seção 4.16) e os diagnósticos do IDE (seção 4.17).

**Fonte:** [Amazon introduces SWE-PolyBench (AWS DevOps Blog)](https://aws.amazon.com/blogs/devops/amazon-introduces-swe-polybench-a-multi-lingual-benchmark-for-ai-coding-agents/) | [Leaderboard](https://amazon-science.github.io/SWE-PolyBench/) | [Paper (arXiv)](https://arxiv.org/abs/2504.08703)

### Características

- 2110+ issues curadas de 21 repositórios reais em 4 linguagens: Java (165), JavaScript (1017), TypeScript (729), Python (199)
- 3 tipos de tarefa: bug fixes, feature requests e refatoração
- Subset SWE-PolyBench500 para experimentação rápida
- Tarefas com maior complexidade que o SWE-Bench: mais arquivos modificados e mais nós alterados por tarefa

### Diferenças em relação ao SWE-Bench

O SWE-Bench, apesar de ser o benchmark de referência para agentes de código, tem limitações: contém apenas repositórios Python, a maioria das tarefas são bug fixes, e o Django representa mais de 45% das tarefas. O SWE-PolyBench foi criado para endereçar essas limitações com diversidade de linguagens, tipos de tarefa e repositórios.

### Métricas de avaliação

1. **Pass Rate** — Proporção de tarefas resolvidas corretamente
2. **File-level Localization** — Capacidade do agente de identificar os arquivos corretos
3. **CST Node-level Retrieval** — Capacidade do agente de identificar as estruturas específicas de código usando Concrete Syntax Tree (CST)

### Recursos

| Recurso | URL |
|---------|-----|
| Leaderboard | https://amazon-science.github.io/SWE-PolyBench/ |
| Dataset (Hugging Face) | https://huggingface.co/collections/AmazonScience/swe-polybench-67f41a0585f1ecaed5fa3aea |
| Código de avaliação (GitHub) | https://github.com/amazon-science/SWE-PolyBench |
| Paper (arXiv) | https://arxiv.org/abs/2504.08703 |
| AWS DevOps Blog | https://aws.amazon.com/blogs/devops/amazon-introduces-swe-polybench-a-multi-lingual-benchmark-for-ai-coding-agents/ |

---

## 9. RECURSOS ADICIONAIS

### 9.1 Links Oficiais

| Recurso | URL |
|---------|-----|
| Site Oficial | https://kiro.dev/ |
| Documentação | https://kiro.dev/docs/ |
| Documentação CLI | https://kiro.dev/docs/cli/ |
| Documentação Web | https://kiro.dev/docs/web/ |
| Kiro Web App | https://app.kiro.dev/ |
| Downloads | https://kiro.dev/downloads/ |
| Changelog | https://kiro.dev/changelog/ |
| Changelog IDE | https://kiro.dev/changelog/ide/ |
| Changelog CLI | https://kiro.dev/changelog/cli/ |
| Changelog Web | https://kiro.dev/changelog/web/ |
| Changelog Models | https://kiro.dev/changelog/models/ |
| Changelog General | https://kiro.dev/changelog/general/ |
| FAQ | https://kiro.dev/faq/ |
| Enterprise | https://kiro.dev/enterprise/ |
| Preços | https://kiro.dev/pricing/ |
| Blog | https://kiro.dev/blog/ |
| GitHub | https://github.com/kirodotdev/Kiro |
| Discord | https://discord.gg/kirodotdev |
| Estudantes | https://kiro.dev/students/ |
| Startups | https://kiro.dev/startups/ |

### 9.2 Documentação Enterprise

| Recurso | URL |
|---------|-----|
| Onboarding Quickstart | https://kiro.dev/docs/enterprise/getting-started/ |
| Conceitos Enterprise | https://kiro.dev/docs/enterprise/concepts/ |
| Identity Provider | https://kiro.dev/docs/enterprise/identity-provider/ |
| IAM Identity Center | https://kiro.dev/docs/enterprise/identity-provider/iam-identity-center/ |
| Okta | https://kiro.dev/docs/enterprise/identity-provider/okta |
| Microsoft Entra ID | https://kiro.dev/docs/enterprise/identity-provider/microsoft-entra |
| Regiões Suportadas | https://kiro.dev/docs/enterprise/supported-regions/ |
| Assinaturas | https://kiro.dev/docs/enterprise/subscribe |
| Billing Enterprise | https://kiro.dev/docs/enterprise/billing/ |
| Governança | https://kiro.dev/docs/enterprise/governance/ |
| Governança de Modelos | https://kiro.dev/docs/enterprise/governance/model/ |
| Governança de MCP | https://kiro.dev/docs/enterprise/governance/mcp/ |
| Gerenciamento de Assinaturas | https://kiro.dev/docs/enterprise/subscription-management/ |
| Monitoramento e Rastreamento | https://kiro.dev/docs/enterprise/monitor-and-track/ |
| Configurações | https://kiro.dev/docs/enterprise/settings/ |
| IAM | https://kiro.dev/docs/enterprise/iam/ |

### 9.3 Documentação de Funcionalidades

| Recurso | URL |
|---------|-----|
| Specs | https://kiro.dev/docs/specs/ |
| Feature Specs — Requirements-first | https://kiro.dev/docs/specs/feature-specs/requirements-first/ |
| Feature Specs — Tech Design-first | https://kiro.dev/docs/specs/feature-specs/tech-design-first/ |
| Quick Plan | https://kiro.dev/docs/specs/quick-plan/ |
| Analyze Requirements | https://kiro.dev/docs/specs/analyze-requirements/ |
| Bugfix Specs | https://kiro.dev/docs/specs/bugfix-specs/ |
| Correctness (PBT) | https://kiro.dev/docs/specs/correctness/ |
| Best Practices (Specs) | https://kiro.dev/docs/specs/best-practices/ |
| Hooks | https://kiro.dev/docs/hooks/ |
| Hook Types | https://kiro.dev/docs/hooks/types/ |
| Hook Actions | https://kiro.dev/docs/hooks/actions/ |
| Hook Best Practices | https://kiro.dev/docs/hooks/best-practices/ |
| Hook Examples | https://kiro.dev/docs/hooks/examples/ |
| Agent Skills | https://kiro.dev/docs/skills/ |
| Skills no CLI | https://kiro.dev/docs/cli/skills/ |
| Steering | https://kiro.dev/docs/steering/ |
| Powers | https://kiro.dev/docs/powers/ |
| MCP Configuration | https://kiro.dev/docs/mcp/configuration/ |
| MCP Server Directory | https://kiro.dev/docs/mcp/servers/ |
| MCP Tool Search (CLI) | https://kiro.dev/docs/cli/mcp/tool-search/ |
| MCP Security | https://kiro.dev/docs/mcp/security/ |
| Modelos | https://kiro.dev/docs/models/ |
| Terminal UI (CLI) | https://kiro.dev/docs/cli/terminal-ui/ |
| Terminal UI vs Classic | https://kiro.dev/docs/cli/terminal-ui/comparison/ |
| Headless Mode (CLI) | https://kiro.dev/docs/cli/headless/ |
| Rewind (CLI) | https://kiro.dev/docs/cli/chat/rewind/ |
| Effort / Reasoning Effort (CLI) | https://kiro.dev/docs/cli/chat/effort/ |
| In-session Settings (CLI) | https://kiro.dev/docs/cli/chat/settings/ |
| Custom Extension Registry | https://kiro.dev/docs/editor/extension-registry/ |
| Subagents | https://kiro.dev/docs/chat/subagents/ |
| Checkpointing | https://kiro.dev/docs/chat/checkpoints/ |
| Summarization | https://kiro.dev/docs/chat/summarization/ |
| Slash Commands | https://kiro.dev/docs/chat/slash-commands/ |
| Dev Servers | https://kiro.dev/docs/chat/dev-servers/ |
| Supervised Mode | https://kiro.dev/docs/chat/autopilot/ |
| Multi-root Workspaces | https://kiro.dev/docs/editor/multi-root-workspaces/ |

### 9.4 Kiro Web (Preview)

| Recurso | URL |
|---------|-----|
| Overview | https://kiro.dev/docs/web/ |
| Setup | https://kiro.dev/docs/web/setup/ |
| Using the Agent | https://kiro.dev/docs/web/using-the-agent/ |
| Autonomous Mode | https://kiro.dev/docs/web/autonomous-mode/ |
| Web Steering | https://kiro.dev/docs/web/steering/ |
| Sandbox | https://kiro.dev/docs/web/sandbox/ |
| GitHub Integration | https://kiro.dev/docs/web/github/ |
| Identity Center Setup | https://kiro.dev/docs/web/identity-center/ |

### 9.5 Conformidade e Legal

| Documento | URL |
|-----------|-----|
| Site Terms | https://aws.amazon.com/terms/ |
| License | https://kiro.dev/license/ |
| Responsible AI Policy | https://aws.amazon.com/ai/responsible-ai/policy/ |
| Privacy Policy | https://aws.amazon.com/privacy/ |
| AWS Compliance Programs | https://aws.amazon.com/compliance/programs/ |
| AWS Data Privacy | https://aws.amazon.com/compliance/data-privacy/ |

---

## HISTÓRICO DE VERSÕES DO KIRO

### IDE Changelog (Resumo)

| Versão | Data | Destaques |
|--------|------|-----------|
| 0.12.155 | May 6, 2026 | Parallel Task Execution, Quick Plan, Analyze Requirements |
| 0.11 | Mar 11, 2026 | MCP Registry Governance, Model Governance, Document Attachments |
| 0.10 | Feb 18, 2026 | Design-First Specs, Bugfix Specs, Hunk-Based Review, Task Hooks, MCP Prompts |
| 0.9.40 | Feb 12, 2026 | Suporte a Okta e Microsoft Entra ID |
| 0.9 | Feb 5, 2026 | Custom Subagents, Agent Skills, Pre/Post Tool Use Hooks, Custom Extension Registry |
| 0.8 | Dec 18, 2025 | Web Tools, Subagents, Contextual Hooks, Per-File Code Review |
| 0.7 | Dec 3, 2025 | Powers, Summarization, Slash Commands |
| 0.6 | Nov 17, 2025 | Spec Correctness (PBT), Kiro CLI, Enterprise, Multi-root Workspaces, Checkpointing |
| 0.5 | Oct 31, 2025 | Remote MCP, Global Steering, AGENTS.md, One-Click MCP Install |
| 0.4 | Oct 15, 2025 | Dev Servers, Spec MVP Tasks, Per Prompt Usage |
| 0.3 | Sep 29, 2025 | Diagnostics Tool, Git Commit Messages, Sonnet 4.5 |

### CLI Changelog (Resumo)

| Versão | Data | Destaques |
|--------|------|-----------|
| 2.4.0 | May 20, 2026 | Rewind Conversations, Effort Control, Unified Settings, workspace init 88% mais rápido |
| 2.3.0 | May 12, 2026 | OAuth Client ID para MCP, KIRO_HOME, V2 TUI Keybindings, Agent Output Side Channels |
| 2.2.0 | Apr 27, 2026 | Adaptive Thinking cross-turn, fix MCP subagent dispatch |
| 2.1 | Apr 24, 2026 | Real-Time Shell Streaming, Tool Search, Skills as Slash Commands, Device Flow, RHEL |
| 2.0 | Apr 13, 2026 | Windows Support, Headless Mode, Terminal UI como padrão |
| 1.28.0 | Mar 20, 2026 | Terminal UI (TUI) experimental, `/chat new`, `--list-models` |
| 1.27 | Mar 2, 2026 | Simplified Agent Creation, Granular Tool Trust, Session Settings |
| 1.26.0 | Feb 13, 2026 | File References (@path), Dynamic Model Selection, Tool Context Insights |
| 1.25.1 | Feb 12, 2026 | Suporte a Okta e Microsoft Entra ID |
| 1.25.0 | Feb 4, 2026 | ACP Support, Help Agent, Web Tools Governance, Subagent Access Control |
| 1.24.0 | Jan 16, 2026 | Skills, Custom Diff Tools, AST Pattern Tools, Code Intelligence (18 langs), Conversation Compaction |
| 1.23.0 | Dec 18, 2025 | Subagents, Plan Agent, Grep/Glob Tools, Multi-Session, MCP Registry |
| 1.22.0 | Dec 11, 2025 | Code Intelligence (LSP), Knowledge Index |
| 1.21.0 | Nov 25, 2025 | Web Search and Fetch |
| 1.20.0 | Nov 17, 2025 | Lançamento do Kiro CLI |

### Web Changelog (Resumo)

| Data | Destaque |
|------|----------|
| May 18, 2026 | Stop Control mid-task, Session Stability, Mobile Layout fixes |
| May 7, 2026 | Lançamento do Kiro Web (Preview) — modos Colaborativo e Autônomo, GitHub-native, sandbox isolado |

### Models Changelog (Resumo)

| Data | Destaque |
|------|----------|
| May 7, 2026 | Claude Opus 4.7 com Adaptive Thinking (geral para Pro/Pro+/Power e IAM Identity Center) |
| Apr 16, 2026 | Claude Opus 4.7 (experimental, IAM Identity Center) |
| Apr 2, 2026 | GLM-5 (experimental) |

### General Changelog (Resumo)

| Data | Destaque |
|------|----------|
| Apr 23, 2026 | Contagem de mensagens por modelo em relatórios de atividade |
| Apr 13, 2026 | E-mails de usuários no console Kiro (IAM Identity Center) |
| Mar 27, 2026 | Download de dados de assinatura como CSV |
| Mar 18, 2026 | Kiro para Estudantes (1.000 créditos/mês por 12 meses) |
| Feb 18, 2026 | Suporte a AWS GovCloud (US-East e US-West) |

---

**Documento compilado em:** Maio 2026
**Versão:** 7.1
**Fonte:** Documentação oficial em [kiro.dev/docs](https://kiro.dev/docs/)

**Nota:** Este documento foi compilado a partir de informações extraídas da documentação oficial do Kiro (kiro.dev/docs) e dos changelogs oficiais (kiro.dev/changelog). Para informações mais recentes e detalhadas, consulte sempre a documentação oficial. Conteúdo foi parafraseado para conformidade com restrições de licenciamento.

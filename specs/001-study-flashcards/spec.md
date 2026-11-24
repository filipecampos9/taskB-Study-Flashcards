# Feature Specification: Study Flashcards

**Feature Branch**: `001-study-flashcards`

**Created**: 2026-11-24

**Status**: Draft

**Input**: User description: "Quero uma aplicação "Study Flashcards". O utilizador estuda um baralho com pelo menos 8 cartões, cada um com frente e verso. Clicar no cartão vira-o. Cada cartão pode ser marcado como "sabido" ou "a rever". O baralho pode ser baralhado. O utilizador vê o progresso ao longo do baralho. No fim vê um resumo (sabidos vs. a rever) e um botão para recomeçar. Tem de ser visualmente atraente e responsiva."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Estudar um cartão de cada vez (Priority: P1)

O utilizador abre a aplicação e vê o primeiro cartão do baralho com a frente visível (pergunta
ou termo). Clica no cartão para o virar e ver o verso (resposta). Depois marca o cartão como
"sabido" ou "a rever" e passa automaticamente ao cartão seguinte, até chegar ao fim do baralho.

**Why this priority**: é o núcleo da aplicação; sem isto não há estudo.

**Independent Test**: abrir a aplicação, virar o primeiro cartão, marcá-lo e confirmar que
aparece o segundo cartão com a frente visível.

**Acceptance Scenarios**:

1. **Given** a aplicação acabou de abrir, **When** a página carrega, **Then** vê-se o cartão 1
   do baralho com a frente visível.
2. **Given** um cartão com a frente visível, **When** o utilizador clica no cartão, **Then** o
   cartão vira e mostra o verso.
3. **Given** um cartão com o verso visível, **When** o utilizador clica novamente no cartão,
   **Then** o cartão volta a mostrar a frente.
4. **Given** um cartão já virado pelo menos uma vez, **When** o utilizador escolhe "Sabido" ou
   "A rever", **Then** a marca fica registada e aparece o cartão seguinte com a frente visível.
5. **Given** o foco do teclado está no cartão, **When** o utilizador prime Espaço ou Enter,
   **Then** o cartão vira, tal como com um clique.

---

### User Story 2 - Ver o progresso e o resumo final (Priority: P2)

Enquanto estuda, o utilizador vê em que posição está no baralho. Ao marcar o último cartão,
vê um resumo com o número de cartões sabidos e a rever, e um botão para recomeçar.

**Why this priority**: dá sentido de avanço e fecho à sessão de estudo; depende da US1.

**Independent Test**: percorrer todo o baralho marcando alguns cartões como "sabido" e outros
como "a rever" e confirmar que o indicador avança e que o resumo mostra as contagens corretas.

**Acceptance Scenarios**:

1. **Given** o utilizador está no cartão N de um baralho de T cartões, **When** olha para o
   ecrã, **Then** vê o texto "N / T" e uma barra de progresso proporcional.
2. **Given** o utilizador está no último cartão, **When** o marca, **Then** em vez de um novo
   cartão aparece o ecrã de resumo.
3. **Given** foram marcados S cartões como "sabido" e R como "a rever", **When** o resumo
   aparece, **Then** mostra S sabidos e R a rever, com S + R = T.
4. **Given** o resumo está visível, **When** o utilizador olha para ele, **Then** vê a lista
   dos cartões marcados "a rever" (frente de cada um).
5. **Given** o resumo está visível, **When** o utilizador ativa "Recomeçar", **Then** volta ao
   cartão 1 com todas as marcas limpas e o progresso a 1 / T.

---

### User Story 3 - Baralhar o baralho (Priority: P3)

O utilizador pode baralhar os cartões para estudar numa ordem diferente, evitando decorar a
sequência.

**Why this priority**: melhora o estudo mas a aplicação é útil sem isto.

**Independent Test**: anotar a ordem das frentes, ativar "Baralhar" e confirmar que a sessão
recomeça com os mesmos cartões numa ordem diferente.

**Acceptance Scenarios**:

1. **Given** qualquer momento da sessão de estudo ou o resumo, **When** o utilizador ativa
   "Baralhar", **Then** a sessão recomeça no cartão 1 de uma nova ordem, com marcas limpas.
2. **Given** um baralho de T cartões, **When** é baralhado, **Then** contém exatamente os mesmos
   T cartões, sem repetidos nem em falta.
3. **Given** um baralho com 8 ou mais cartões, **When** é baralhado, **Then** a nova ordem é
   diferente da ordem imediatamente anterior.

---

### Edge Cases

- Utilizador tenta marcar antes de virar o cartão: os botões "Sabido" / "A rever" estão
  desativados até o cartão ser virado pelo menos uma vez.
- Utilizador recarrega a página a meio: a sessão recomeça do início (sem persistência).
- Texto longo no verso: o conteúdo continua legível dentro do cartão, sem sair dos limites,
  num ecrã de 320 px de largura.
- Todos os cartões marcados "sabido": o resumo mostra R = 0 e uma mensagem a indicar que não há
  cartões a rever, em vez de lista vazia.
- Utilizador com preferência de movimento reduzido: o cartão vira sem animação de rotação.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: O baralho MUST conter pelo menos 8 cartões, cada um com frente e verso de texto.
- **FR-002**: O conteúdo dos cartões MUST estar definido separadamente da lógica da aplicação,
  de forma a poder ser editado sem alterar o comportamento.
- **FR-003**: A aplicação MUST mostrar um cartão de cada vez, começando pela frente.
- **FR-004**: Clicar/tocar no cartão MUST alternar entre frente e verso.
- **FR-005**: O cartão MUST poder ser virado com teclado (Espaço e Enter quando focado).
- **FR-006**: Os utilizadores MUST poder marcar o cartão atual como "Sabido" ou "A rever",
  depois de o terem virado pelo menos uma vez.
- **FR-007**: Marcar um cartão MUST registar a marca e avançar para o cartão seguinte, ou para
  o resumo se for o último.
- **FR-008**: A aplicação MUST mostrar o progresso como "posição / total" e uma barra
  proporcional, atualizados a cada avanço.
- **FR-009**: No fim do baralho, a aplicação MUST mostrar um resumo com o número de cartões
  sabidos, o número a rever, e a lista das frentes dos cartões a rever.
- **FR-010**: O resumo MUST ter um botão "Recomeçar" que volta ao cartão 1, mantendo a ordem
  atual e limpando todas as marcas.
- **FR-011**: A aplicação MUST ter uma ação "Baralhar", disponível durante a sessão e no resumo,
  que reordena aleatoriamente os cartões e recomeça a sessão com marcas limpas.
- **FR-012**: A interface MUST ser utilizável sem scroll horizontal em ecrãs de 320 px a
  1920 px de largura.
- **FR-013**: Todos os controlos MUST ser acessíveis por teclado, com foco visível, e o texto
  MUST cumprir contraste WCAG AA.
- **FR-014**: O virar do cartão MUST ter uma transição visual animada, exceto quando o
  utilizador tem preferência de movimento reduzido.
- **FR-015**: A interface MUST usar uma identidade visual consistente: paleta de cores definida,
  uma família tipográfica para títulos e texto, e cores distintas para "Sabido" e "A rever"
  que não dependem só da cor (também texto ou ícone).
- **FR-016**: Mudanças de cartão e o aparecimento do resumo MUST ser anunciados a leitores de
  ecrã.

### Key Entities

- **Cartão**: unidade de estudo; tem frente (pergunta/termo) e verso (resposta/definição).
- **Baralho**: coleção ordenada de cartões (mínimo 8); a ordem muda ao baralhar.
- **Sessão de estudo**: passagem pelo baralho; guarda a posição atual, se o cartão atual já foi
  virado, e a marca ("sabido" / "a rever") de cada cartão já avaliado. Termina no resumo.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Um utilizador novo consegue virar e marcar o primeiro cartão em menos de 15
  segundos, sem instruções.
- **SC-002**: Uma sessão completa (todos os cartões até ao resumo) pode ser feita só com
  teclado, sem usar rato nem toque.
- **SC-003**: Em 100% das sessões, as contagens do resumo somam o total de cartões e
  correspondem às marcas dadas.
- **SC-004**: A aplicação é totalmente utilizável num telemóvel de 320–414 px de largura em
  orientação vertical: todos os textos legíveis e todos os botões tocáveis sem zoom.
- **SC-005**: A página fica pronta a usar em menos de 2 segundos numa ligação móvel típica (4G).
- **SC-006**: Numa revisão visual, os ecrãs de estudo e de resumo usam a mesma paleta e
  tipografia, e nenhum texto falha o contraste AA numa ferramenta de verificação de contraste.

## Assumptions

- Existe um único baralho, sem escolha entre baralhos; o tema do conteúdo inicial será definido
  no planeamento.
- O conteúdo é apenas texto (sem imagens nem áudio).
- Não há persistência entre visitas: recarregar a página recomeça a sessão.
- Não há navegação para trás nem possibilidade de alterar uma marca já dada; para refazer, o
  utilizador recomeça ou baralha.
- Não há contas de utilizador, nem criação/edição de cartões na interface.
- A interface é em português.
- Fora de âmbito: repetição espaçada, estudar apenas os cartões "a rever", estatísticas entre
  sessões.

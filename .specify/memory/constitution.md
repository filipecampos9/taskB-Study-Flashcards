<!--
Sync Impact Report
- Version change: (template) → 1.0.0
- Modified principles: n/a (primeira ratificação; placeholders substituídos)
- Added principles:
  I. Simplicidade e Dependências Mínimas
  II. Código Legível e Organizado
  III. Interface Responsiva (Mobile-First)
  IV. Acessibilidade Básica
  V. Dados Separados da Lógica
  VI. Requisitos Verificáveis Manualmente
- Added sections: Restrições Técnicas e de Publicação; Fluxo de Desenvolvimento e Verificação
- Removed sections: nenhuma
- Templates (.specify/templates/*): não alterados; leem a constituição em tempo de execução
- Follow-up TODOs: nenhum
-->

# Study Flashcards Constitution

## Core Principles

### I. Simplicidade e Dependências Mínimas

- A aplicação MUST ser construída com HTML, CSS e JavaScript nativos do browser sempre que
  estes resolvam o problema.
- Cada dependência externa (biblioteca, framework, ferramenta de build) MUST ser justificada
  por escrito no plano da funcionalidade, indicando porque a plataforma nativa não basta.
- Abstrações, configuração ou código "para o futuro" MUST NOT ser introduzidos sem um requisito
  atual que os exija (YAGNI).

**Justificação**: um projeto pequeno ganha mais em manutenção e tempo de carregamento do que
perde em conveniência ao evitar dependências.

### II. Código Legível e Organizado

- Ficheiros MUST ter responsabilidade clara (estrutura em HTML, estilo em CSS, comportamento
  em JS); não se mistura estilo inline nem lógica em atributos HTML salvo justificação.
- Nomes de funções, variáveis e classes MUST descrever a sua intenção; funções MUST ser curtas
  e fazer uma coisa.
- Formatação MUST ser consistente em todo o projeto.

**Justificação**: o código deve ser compreensível por quem o lê pela primeira vez, sem
explicação adicional.

### III. Interface Responsiva (Mobile-First)

- A interface MUST ser utilizável em ecrãs a partir de 320 px de largura sem scroll horizontal.
- Alvos de toque MUST ter pelo menos 44×44 px.
- O layout MUST adaptar-se de telemóvel a desktop usando CSS (media queries, flexbox, grid),
  sem duplicar conteúdo.

**Justificação**: o estudo com flashcards acontece frequentemente no telemóvel.

### IV. Acessibilidade Básica

- Texto MUST cumprir contraste mínimo WCAG AA (4.5:1 texto normal, 3:1 texto grande).
- Todas as ações MUST ser executáveis só com teclado, com ordem de foco lógica e foco visível.
- Elementos interativos MUST usar elementos HTML semânticos (`button`, `a`, `input`) ou
  ter papel e nome acessível equivalentes.
- A página MUST declarar `lang` e ter títulos estruturados.

**Justificação**: acessibilidade básica tem custo baixo quando feita desde o início.

### V. Dados Separados da Lógica

- O conteúdo (baralhos, cartões, textos) MUST viver em ficheiro(s) de dados próprios (ex.: JSON
  ou módulo JS só com dados), nunca embutido nas funções de lógica ou no HTML.
- Adicionar ou editar conteúdo MUST ser possível sem alterar código de lógica.

**Justificação**: permite atualizar o material de estudo sem risco de partir a aplicação.

### VI. Requisitos Verificáveis Manualmente

- Cada requisito na especificação MUST ter critério de aceitação observável, verificável por uma
  pessoa no browser em passos concretos (ex.: "ao premir Espaço, o cartão vira").
- Requisitos vagos ("rápido", "intuitivo", "bonito") MUST ser reformulados em critérios
  observáveis ou removidos.
- Testes automáticos são opcionais; a verificação manual documentada é o critério de aceitação.

**Justificação**: garante que "feito" tem significado objetivo num projeto sem suite de testes.

## Restrições Técnicas e de Publicação

- Aplicação de página única, estática, sem backend nem base de dados remota.
- Publicação no Netlify como site estático; se houver passo de build, MUST produzir apenas
  ficheiros estáticos.
- Persistência, se necessária, MUST ser feita no browser (ex.: `localStorage`).
- A aplicação MUST funcionar nas versões atuais de Chrome, Firefox e Safari (desktop e mobile).

## Fluxo de Desenvolvimento e Verificação

- Cada funcionalidade segue o fluxo Spec Kit: especificar → planear → tarefas → implementar.
- O plano de cada funcionalidade MUST incluir uma verificação de conformidade com esta
  constituição (Constitution Check).
- Antes de dar uma funcionalidade por concluída, MUST ser executada a lista de verificação manual
  dos seus critérios de aceitação, incluindo um teste em largura de telemóvel e um percurso
  completo só com teclado.

## Governance

- Esta constituição prevalece sobre outras práticas do projeto; desvios MUST ser justificados
  por escrito no plano da funcionalidade afetada.
- Alterações à constituição MUST ser feitas via `/speckit-constitution`, com Sync Impact Report
  e incremento de versão.
- Versionamento semântico: MAJOR para remoção ou redefinição incompatível de princípios; MINOR
  para novos princípios ou secções, ou orientação materialmente alargada; PATCH para
  clarificações e correções de redação.
- Revisões de código e de especificação MUST verificar conformidade com os princípios I–VI.

**Version**: 1.0.0 | **Ratified**: 2026-11-24 | **Last Amended**: 2026-11-24

# Checklist para Desenvolvimento Assistido por IA (DAIA)

> por [Vinicius Cardoso Garcia](https://viniciusgarcia.me) (vcg@cin.ufpe.br)

**versão**: 2025-07-08-2336

Este documento serve como um guia de boas práticas para o desenvolvimento de software em nosso time como material complementar à disciplina [Transformação Digital com IA: Utilizando Modelos de Linguagem no Ambiente de Negócios](https://dev.to/vinicius3w/series/32001). Ele foi criado para ser usado em conjunto com ferramentas de IA generativa, como o Claude Code, GitHub Copilot, ou similares.

**Lembre-se:** A IA é um **copiloto**, não o piloto. Ela acelera nosso trabalho, sugere melhorias e nos ajuda a identificar problemas, mas a responsabilidade final pela qualidade, segurança e manutenibilidade do código é sempre do **desenvolvedor**. Use este checklist para guiar suas interações com a IA e para revisar criticamente o código gerado por ela e por você mesmo. O objetivo é criar software robusto, e não apenas entregar funcionalidades rapidamente.

Cada prática, tem seu nível de maturidade classificado como:

- 🟢 **Fundamental** (todos devem seguir)    
- 🟡 **Intermediário** (importante, mas exige mais experiência)    
- 🔵 **Avançado** (útil, mas requer avaliação de custo-benefício)

**Para Desenvolvedores Juniores**
- **Sempre** execute os prompts sugeridos antes de considerar uma tarefa completa
- **Leia** as seções "Impacto no mundo real" para entender o contexto
- **Peça ajuda** aos seniores quando os prompts identificarem problemas complexos

**Para Desenvolvedores Plenos e Seniores**
- **Adapte** os prompts para contextos específicos do projeto
- **Revise** as sugestões da IA antes de implementar
- **Mentore** juniores nos pontos identificados pelos prompts

## Como e Quando Usar este Checklist

Para ser prático, o time precisa saber _quando_ aplicar essas verificações.

**Fluxo de Trabalho Sugerido:**
 
 1. **Durante o Desenvolvimento:** Use os prompts da IA de forma proativa enquanto codifica para evitar problemas comuns.
 2. **Antes do Commit:** Faça uma autoavaliação rápida usando os itens de `VERIFICAÇÕES` mais relevantes para a sua tarefa.
 3. **Na Revisão de Pull Request (PR):** Tanto o autor quanto o revisor devem usar este checklist como um guia para a revisão de código. O revisor pode, inclusive, usar os prompts para sugerir melhorias concretas no PR.

## 🔧 Boas Práticas de Código

### 1\. Evitar Duplicação de Código (DRY - Don't Repeat Yourself)
**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Evitar a repetição desnecessária de código para garantir melhor manutenção, testabilidade e evolução da base de código. O princípio DRY busca promover reutilização e organização do conhecimento dentro do sistema.

**✅ VERIFICAÇÕES**

- Verificar se funções comuns estão em componentes ou hooks reutilizáveis
- Confirmar que padrões repetitivos foram abstraídos em componentes compartilhados

> [!NOTE]
> Código duplicado é um dos principais indicadores de design de software deficiente. Quando existem múltiplas cópias do mesmo código, fica difícil manter e evoluir o software, pois cada alteração precisa ser feita em todos os lugares onde o código foi duplicado.


> 💡 **Exemplo real**:
> Uma empresa de comércio eletrônico tinha o mesmo código de manipulação de carrinho repetido em 7 locais diferentes. Quando precisaram adicionar cupons de desconto, a implementação falhou em 3 desses locais por esquecimento, causando inconsistências que frustraram os clientes e geraram perdas financeiras.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Identifique padrões de código duplicados no projeto. Procure por funções, componentes ou blocos
de código que aparecem em vários lugares com pouca ou nenhuma alteração. Sugira refatorações para
criar componentes reutilizáveis, hooks personalizados ou funções utilitárias que possam substituir
essa duplicação, seguindo o princípio DRY (Don't Repeat Yourself).
```

### 2\. Eliminar Código Não Utilizado (Dead Code)

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Remover código morto — ou seja, qualquer trecho que não é utilizado durante a execução da aplicação — para reduzir complexidade, melhorar performance e facilitar a manutenção do projeto.

**✅ VERIFICAÇÕES**

- Verificar se existem componentes, funções ou imports que não são usados
- Confirmar que não há código comentado sem propósito claro

> [!NOTE]
> Código não utilizado aumenta o tamanho do bundle JavaScript desnecessariamente, impactando o tempo de carregamento das páginas e a experiência do usuário.

>💡 **Exemplo real**:
> Uma startup de tecnologia financeira descobriu que quase 30% do seu bundle JavaScript era composto por código nunca executado ou importações não utilizadas. Após uma limpeza sistemática, o tempo de carregamento inicial da aplicação foi reduzido em 45%, melhorando significativamente as métricas de engajamento dos usuários e a taxa de conversão de clientes.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Analise o projeto e identifique: 1) Componentes que foram criados mas nunca importados ou
renderizados, 2) Funções declaradas que nunca são chamadas, 3) Importações que não são utilizadas,
4) Variáveis de estado (useState) que nunca mudam ou nunca são lidas, 5) Código comentado sem
explicação clara de por que foi mantido. Sugira a remoção desses elementos para melhorar a
manutenibilidade e performance do código.
```

### 3\. Uso Consistente de TypeScript

**Nível:** 🟡 Intermediário

**🎯 OBJETIVO**

Aproveitar todo o poder do TypeScript para detectar erros em tempo de desenvolvimento, garantir segurança de tipos e melhorar a documentação implícita do código. Evita comportamentos imprevisíveis ao substituir o uso genérico de `any` por tipos explícitos e consistentes.

**✅ VERIFICAÇÕES**

- Confirmar que tipos estão sendo usados corretamente e não há uso excessivo de `any`
- Verificar se interfaces e tipos estão bem definidos e organizados
- Avaliar consistência no uso de `interface` vs `type`

> [!NOTE]
> O uso inconsistente de tipos ou confiar demais no tipo `any` elimina as principais vantagens do TypeScript e aumenta o risco de bugs silenciosos.

> 💡 **Exemplo real**:
> Uma equipe de desenvolvimento gastou três dias depurando um erro que poderia ter sido capturado durante o desenvolvimento se os tipos apropriados tivessem sido usados. O bug surgiu porque uma API retornava valores em um formato ligeiramente diferente do esperado, e como o código usava 'any', o TypeScript não alertou sobre essas discrepâncias que eventualmente quebraram funcionalidades críticas na aplicação.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Examine o uso de tipos no projeto. Identifique: 1) Uso excessivo do tipo 'any' que deve ser
substituído por tipos específicos, 2) Props de componentes que não têm interfaces ou tipos
definidos, 3) Inconsistências no uso de 'interface' vs 'type', 4) Tipos que poderiam ser mais
específicos ou restritivos. Sugira melhorias para aproveitar melhor o sistema de tipos do
TypeScript e aumentar a segurança do código.
```

### 4\. Componentes Bem Estruturados

**Nível:** 🟡 Intermediário

**🎯 OBJETIVO**

Garantir que os componentes React sejam coesos, com responsabilidade única e legibilidade adequada. Componentes menores e bem definidos facilitam testes, manutenção, reutilização e leitura por outros membros do time.

**✅ VERIFICAÇÕES**

- Verificar se os componentes seguem o princípio de responsabilidade única
- Confirmar que componentes grandes foram divididos em subcomponentes menores
- Avaliar se o JSX está legível e não excessivamente aninhado

> [!NOTE]
> Componentes grandes e complexos são difíceis de entender, testar e manter, o que prejudica a escalabilidade do sistema.

> 💡 **Exemplo real**:
> Uma empresa de software tinha um componente de painel administrativo com mais de 2.000 linhas que fazia tudo, desde autenticação até visualização de dados e gerenciamento de usuários. Ninguém ousava modificá-lo porque era impossível prever os efeitos colaterais de qualquer mudança. Após refatorar em 15 componentes menores, o tempo para implementar novos recursos diminuiu em 70% e os bugs relatados caíram significativamente.


**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Identifique componentes React que violam o princípio de responsabilidade única ou são
excessivamente grandes. Procure por: 1) Componentes com mais de 250 linhas de código, 2)
Componentes que fazem muitas coisas diferentes, 3) JSX complexo ou profundamente aninhado.
Sugira como estes componentes podem ser divididos em componentes menores, mais focados e
reutilizáveis, explicando os benefícios para manutenção e legibilidade.
```

### 5\. Gerenciamento de Estado Eficiente

**Nível:** 🟡 Intermediário

**🎯 OBJETIVO**

Garantir que o estado dos componentes React seja controlado de forma clara, localizada e eficiente. O bom gerenciamento de estado evita acoplamento desnecessário, melhora a performance e facilita a manutenção e a extensibilidade da aplicação.

**✅ VERIFICAÇÕES**

- Confirmar que o estado está sendo gerenciado no nível apropriado
- Verificar se não há prop drilling excessivo ou estado duplicado
- Avaliar se Context API, Zustand, Redux ou outras soluções são utilizadas adequadamente
- Avaliar se a ferramenta de estado global (Context, Redux, Zustand, etc.) é a correta para a necessidade. O Context API é ideal para dados que mudam com pouca frequência.

> [!NOTE]
> Um gerenciamento de estado ineficiente leva a componentes acoplados e difíceis de reutilizar. . Também pode causar re-renderizações excessivas e confusas.

> 💡 **Exemplo real**:
> Uma aplicação de calendário compartilhava o estado de eventos através de 6 níveis de componentes, tornando qualquer alteração na estrutura um pesadelo de refatoração. Ao identificar quais estados deveriam ser globais (usando Context) e quais deveriam ser locais, a aplicação se tornou muito mais modular, facilitando a implementação de novos recursos como visualizações alternativas do calendário e filtros personalizados.


**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Analise o gerenciamento de estado na aplicação. Identifique: 1) Casos de
"prop drilling" excessivo (passar props através de muitos componentes),
2) Estado que deveria estar em um nível superior da árvore de
componentes, 3) Estado duplicado em vários componentes, 4) Uso inadequado
de Context API para dados que não precisam ser globais. Sugira a estratégia mais simples
 que resolva o problema, explicando por que `useState` local, elevação de estado
(`lifting state up`), `useContext` ou uma biblioteca externa como Zustand/Redux seria a melhor
escolha em cada caso.
```

### 6\. Uso Adequado de Hooks React

**Nível:** 🟡 Intermediário

**🎯 OBJETIVO**

Garantir o uso correto e seguro dos React Hooks, evitando bugs relacionados ao ciclo de vida de componentes, à ordem de execução e à memoização. Hooks bem utilizados promovem reutilização de lógica, clareza e previsibilidade no comportamento da aplicação.

**✅ VERIFICAÇÕES**

- Verificar se as regras dos hooks estão sendo seguidas
- Confirmar que hooks personalizados são usados para lógica reutilizável
- Avaliar uso correto de `useEffect`, `useMemo`, `useCallback`, `useReducer`

> [!NOTE]
> O uso incorreto de hooks pode levar a bugs difíceis de detectar, especialmente.

> 💡 **Exemplo real**:
> Uma empresa de software estava enfrentando um problema sério em uma aplicação de análise de dados onde certos gráficos oscilavam constantemente devido a renderizações infinitas. O problema foi causado por dependências incorretas em um `useEffect`, onde cada atualização de estado desencadeava novamente o efeito. Após a correção adequada das dependências e extração da lógica para hooks personalizados, a aplicação ficou estável e mais previsível.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Analise o uso de hooks React no projeto. Identifique: 1) Violações das
regras de hooks (chamadas condicionais, dentro de loops), 2) Dependências
ausentes ou desnecessárias em useEffect/useMemo/useCallback, 3) Lógica
complexa que poderia ser extraída para hooks personalizados, 4) Uso
excessivo de useState quando useReducer seria mais apropriado. Sugira
melhorias para seguir as melhores práticas de hooks e tornar o código
mais previsível e testável.
```

## 🎨 Arquitetura e Organização

### 7\. Separação de Lógica e Apresentação

**Nível:** 🟡 Intermediário

**🎯 OBJETIVO**

Promover a separação clara entre a lógica de negócios e a camada de apresentação da interface. Isso facilita testes unitários, reutilização de componentes visuais e manutenção do sistema, seguindo o padrão container/presentational.

**✅ VERIFICAÇÕES**

- Confirmar que componentes de apresentação não contêm lógica complexa
- - Verificar se chamadas de API, validações e manipulações de dados estão isoladas em containers ou hooks
- Avaliar se há componentes genéricos reutilizáveis desacoplados do domínio da aplicação

> [!NOTE]
> Misturar lógica de negócio com código de interface prejudica a legibilidade, dificulta a reutilização e torna os testes mais frágeis e complexos.

> 💡 **Exemplo real**:
> Um aplicativo de reservas tinha a lógica de validação, chamadas de API e renderização UI tudo nos mesmos componentes. Isso tornava impossível reutilizar a interface em outros contextos ou testar a lógica isoladamente. Após adotar o padrão container/presentational, a empresa conseguiu criar uma biblioteca de componentes visual que acelerou o desenvolvimento de novos recursos em 40% e facilitou a criação de testes automatizados.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Examine a estrutura dos componentes React e identifique onde a separação
entre lógica e apresentação pode ser melhorada. Procure por: 1)
Componentes de UI com regras de negócio embutidas, 2) Chamadas de API
diretamente em componentes de apresentação, 3) Componentes que poderiam
seguir o padrão container/presentational. Sugira refatorações para
melhorar a separação de responsabilidades, tornando os componentes mais
reutilizáveis e testáveis.
```

### 8\. Tratamento Adequado de Erros

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Assegurar que falhas no sistema sejam tratadas de forma apropriada, evitando comportamentos inesperados e fornecendo feedback claro ao usuário. Um bom tratamento de erros melhora a resiliência, facilita o suporte técnico e aumenta a confiança do usuário na aplicação.

**✅ VERIFICAÇÕES**

- Verificar se há tratamento de erros para chamadas de API e operações assíncronas
- Confirmar que erros não causam falhas silenciosas
- Garantir que mensagens de erro sejam claras, úteis e visíveis para o usuário
- Avaliar uso de boundaries de erro no React quando aplicável
- Verificar se existem **estados de carregamento (loading states)** para operações assíncronas, evitando que a UI pareça travada.

> [!NOTE]
> Falhas silenciosas e mensagens de erro obscuras frustram os usuários, aumentam o número de chamados de suporte e dificultam a depuração pela equipe técnica.

> 💡 **Exemplo real**:
> Uma empresa de e-commerce tinha uma alta taxa de abandono de carrinho porque, quando o servidor de pagamento estava sobrecarregado, a aplicação simplesmente travava sem explicação. Ao implementar tratamento adequado de erros com mensagens claras e opções de recuperação, a taxa de conversão aumentou em 15%, mesmo quando ocorriam problemas, porque os usuários entendiam o que estava acontecendo e podiam tentar novamente.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Analise o tratamento de erros na aplicação. Identifique: 1) Chamadas de
API sem blocos try/catch ou tratamento de erros, 2) Operações assíncronas
que podem falhar silenciosamente, 3) Falta de feedback ao usuário quando
erros ocorrem, 4) Erros que são registrados no console mas não tratados
adequadamente. Sugira implementações de boundary errors de React e
estratégias para melhorar a experiência do usuário durante falhas. Além disso,
identifique locais onde a ausência de um estado de carregamento (`loading`) degrada
a experiência do usuário durante operações assíncronas.
```

### 9\. Desempenho e Otimizações

**Nível:** 🔵 Avançado

**🎯 OBJETIVO**

Evitar gargalos de performance que afetam a experiência do usuário, garantindo uma interface responsiva e eficiente. Boas práticas de otimização ajudam a prevenir re-renderizações desnecessárias, atrasos em interações e uso excessivo de recursos, especialmente em dispositivos móveis.

**✅ VERIFICAÇÕES**

- Confirmar uso de memoização (`useMemo`, `useCallback`, `React.memo`) quando apropriado
- Verificar se componentes não re-renderizam sem necessidade
- Avaliar se listas extensas utilizam virtualização (ex: `react-window`, `react-virtualized`)
- Garantir que imagens e mídias estejam otimizadas
- Verificar debounce ou throttle em eventos de digitação e scroll

> [!NOTE]
> Problemas de performance prejudicam diretamente o engajamento e podem levar ao abandono do produto. Otimizações bem aplicadas aumentam a fluidez da aplicação e reduzem o custo de infraestrutura.

> 💡 **Exemplo real**:
> Uma aplicação de visualização de dados mostrava uma lista de 5.000 transações que fazia cada interação travar o navegador por segundos. Ao implementar virtualização de lista e memoização adequada, a aplicação passou a responder instantaneamente. Em outro caso, uma funcionalidade de filtragem em tempo real estava recalculando resultados a cada tecla digitada sem qualquer debounce, causando travamentos em dispositivos móveis — o problema foi resolvido com um simples `useCallback` e controle de eventos com `debounce`.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Identifique problemas de performance e oportunidades de otimização.
Procure por: 1) Componentes que renderizam frequentemente e poderiam usar
React.memo(), 2) Funções criadas em cada renderização que deveriam usar
useCallback(), 3) Cálculos pesados que deveriam usar useMemo(), 4) Listas
grandes sem virtualização, 5) Imagens não otimizadas. Sugira melhorias
concretas para cada problema encontrado, explicando o impacto na
performance.
```

### 10\. Organização e Estrutura do Projeto

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Manter uma estrutura de arquivos e pastas clara, coesa e padronizada, facilitando a navegação, a escalabilidade e a integração de novos membros no time. Uma estrutura bem organizada reduz o tempo de onboarding e minimiza erros em ambientes colaborativos.

**✅ VERIFICAÇÕES**

- Verificar se arquivos e pastas seguem uma estrutura lógica e consistente (por feature, por tipo ou híbrida)
- Confirmar que não há dependências circulares entre módulos
- Avaliar se arquivos muito grandes foram devidamente divididos em partes menores
- Validar organização e ordenação das importações

> [!NOTE]
> Uma estrutura de projeto caótica dificulta a colaboração e aumenta significativamente o tempo de entendimento do código, especialmente para novos desenvolvedores.

> 💡 **Exemplo real**:
> Uma empresa de tecnologia tinha um projeto onde encontrar qualquer arquivo era como uma caça ao tesouro - alguns componentes estavam organizados por tipo, outros por funcionalidade, e alguns simplesmente soltos na raiz. O tempo médio para que um novo desenvolvedor fizesse sua primeira contribuição era de 3 semanas. Após reorganizar o projeto seguindo uma estrutura consistente, novos membros passaram a contribuir em apenas 3 dias, e o tempo para implementar novos recursos diminuiu em 35%.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Analise a estrutura de arquivos e pastas do projeto. Identifique: 1)
Inconsistências na organização (por tipo, por feature ou híbrida), 2)
Dependências circulares entre módulos, 3) Importações desordenadas ou
excessivamente longas, 4) Arquivos muito grandes que deveriam ser
divididos. Sugira melhorias para a estrutura do projeto seguindo boas
práticas para React/TypeScript, explicando como uma melhor organização
facilita a manutenção a longo prazo.
```

## ♿ Qualidade e Acessibilidade

### 11\. Acessibilidade (a11y)

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Garantir que a aplicação possa ser utilizada por todas as pessoas, incluindo aquelas com deficiência visual, motora ou cognitiva. Acessibilidade é uma responsabilidade ética e, em muitos contextos, também uma exigência legal. Promover interfaces inclusivas também melhora a usabilidade geral do sistema.

**✅ VERIFICAÇÕES**

- Confirmar uso adequado de atributos ARIA, semântica HTML e navegação por teclado
- Verificar contraste de cores e tamanho de texto para legibilidade
- Avaliar foco visível em elementos interativos
- Garantir acessibilidade de formulários e componentes customizados

> [!NOTE]
> Falta de acessibilidade afeta diretamente a inclusão digital e pode acarretar sanções legais e danos à reputação da empresa.

> 💡 **Exemplo real**:
> Uma grande empresa de varejo foi processada porque seu site não era acessível para pessoas com deficiência visual, resultando em um acordo de US$ 6 milhões. Problemas comuns incluíam botões sem labels apropriados para leitores de tela, imagens sem texto alternativo e formulários impossíveis de navegar usando apenas o teclado. Além das questões legais, melhorar a acessibilidade frequentemente beneficia todos os usuários com uma interface mais clara e coerente.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Avalie a acessibilidade da aplicação React. Identifique: 1) Elementos
interativos sem rótulos acessíveis, 2) Imagens sem texto alternativo, 3)
Uso incorreto de elementos semânticos HTML, 4) Falha de contraste de
cores, 5) Componentes não navegáveis por teclado. Sugira correções para
tornar a aplicação mais acessível, seguindo as diretrizes WCAG e as
melhores práticas de desenvolvimento React acessível.
```

### 12\. Testes Adequados

**Nível:** 🟡 Intermediário

**🎯 OBJETIVO**

Assegurar que as funcionalidades da aplicação sejam verificadas por meio de testes automatizados robustos e significativos. Um bom conjunto de testes reduz regressões, melhora a confiança nas mudanças e facilita a refatoração segura do código.

**✅ VERIFICAÇÕES**

- Verificar cobertura de testes para componentes e lógica crítica
- Confirmar que testes validam comportamento e não apenas a renderização
- Avaliar uso adequado de mocks e spies
- Evitar testes frágeis que quebram por mudanças irrelevantes
- Garantir testes automatizados em nível unitário, de integração e/ou end-to-end
- Confirmar que os testes verificam o **comportamento** do componente (o que o usuário vê e faz) e não detalhes de **implementação** (como o estado interno é chamado, por exemplo).

> [!NOTE]
> A ausência de testes significativos gera retrabalho e aumenta o custo de manutenção. Testes frágeis ou superficiais passam uma falsa sensação de segurança.

> 💡 **Exemplo real**:
> Uma empresa de software descobriu que cada bug em produção custava 10 vezes mais para corrigir do que se tivesse sido capturado durante o desenvolvimento. Uma equipe implementou um fluxo de trabalho extenso sem testes adequados; seis meses depois, ao tentar adicionar novos recursos, quase todas as alterações quebravam funcionalidades existentes, forçando-os a praticamente reescrever o sistema. Uma estratégia de testes bem implementada poderia ter economizado meses de retrabalho.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Analise a cobertura e qualidade dos testes no projeto. Identifique: 1)
Componentes críticos sem testes, 2) Testes que apenas verificam
renderização sem testar comportamento, 3) Uso inadequado de mocks, 4)
Testes frágeis que quebram facilmente. 5) Avalie se os testes existentes são robustos
ou se estão muito acoplados à implementação interna dos componentes, sugerindo formas
de testar o comportamento observável pelo usuário. Sugira melhorias na estratégia de
testes incluindo testes unitários, de integração e end-to-end onde apropriado,
priorize o que deve ser testado primeiro e como escrever testes mais robustos e
significativos.
```

## 🔒 Segurança para Aplicações

### 13\. Verificar se chaves de API e dados sensíveis estão protegidos

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Garantir que informações sensíveis — como chaves de API, tokens de autenticação, credenciais e dados privados — estejam protegidas e não expostas acidental ou intencionalmente no repositório de código ou na interface do cliente.

**✅ VERIFICAÇÕES**

- Conﬁrme que arquivos como `.env` estão incluídos no `.gitignore`
- Veriﬁque se nenhuma chave de API está diretamente exposta no código-fonte
- Validar se dados sensíveis estão armazenados em variáveis de ambiente e acessados por mecanismos seguros
- Garantir que configurações secretas estejam isoladas por ambiente (dev/staging/prod)

> [!NOTE]
> A exposição de dados sensíveis no código é uma das causas mais comuns de vazamentos e invasões. Quando detectada tarde, pode resultar em prejuízos financeiros severos e sanções legais.

> 💡 **Exemplo real**:
> Uma empresa teve seu código-fonte publicado acidentalmente no GitHub com chaves AWS expostas, resultando em hackers minerando criptomoedas em seus servidores e gerando uma fatura de mais de $6.000 em apenas 12 horas. Outro caso comum é o envio de arquivos `.env` para repositórios públicos, permitindo que qualquer pessoa use as credenciais para acessar serviços pagos ou privados.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Verifique se o arquivo .gitignore existe e se contém entradas para arquivos de
configuração como .env ou arquivos que possam conter credenciais. Também procure
por chaves de API, senhas ou tokens diretamente escritos no código fonte. Confirme
que o projeto usa variáveis de ambiente para dados sensíveis ao invés de valores
codificados diretamente.
```

### 14\. Garantir que o código não está expondo APIs importantes no frontend

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Proteger as APIs da aplicação garantindo que endpoints críticos e chaves de autenticação não sejam acessíveis no ambiente cliente (navegador). Toda comunicação sensível deve passar por uma camada de backend segura.

**✅ VERIFICAÇÕES**

- Certificar-se de que chamadas de API sensíveis não estão visíveis diretamente no código frontend
- Confirmar que nenhuma chave de API é exposta em arquivos JavaScript ou TypeScript enviados ao navegador
- Avaliar se todas as chamadas que envolvem autenticação, lógica de negócios ou manipulação de dados sensíveis passam por um backend intermediário

> [!NOTE]
> APIs expostas no cliente podem ser inspecionadas facilmente por usuários mal-intencionados, facilitando abusos, fraudes e vazamentos de dados.

> 💡 **Exemplo real**: 
> Uma startup de e-commerce expôs sua API de preços no frontend, permitindo que concorrentes criassem scripts para monitorar e subprecificar automaticamente seus produtos. Em outro exemplo, uma API de gerenciamento de usuários exposta no frontend permitiu que hackers listassem todos os emails de clientes, resultando em vazamento de dados pessoais e multas substanciais por violação de privacidade.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Analise o código frontend (JavaScript/TypeScript) e procure por endpoints de API
expostos diretamente no código cliente. Verifique se as chaves de API ou tokens de
autenticação estão sendo usados no código frontend ou se todas as chamadas sensíveis
são feitas através de um backend seguro. Identifique qualquer chamada de API que
expõe endpoints internos ou chaves diretamente no navegador.
```

### 15\. Confirmar validação de entrada de dados

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Assegurar que toda entrada de dados proveniente do usuário seja validada corretamente no frontend e no backend, prevenindo erros de lógica, falhas de segurança e comportamentos inesperados na aplicação.

**✅ VERIFICAÇÕES**

- Verificar se campos de formulários possuem validação de tipo, formato e limites
- Confirmar que não é possível enviar dados maliciosos ou inválidos para a aplicação
- Validar se há tratamento para entradas inesperadas (ex: campos vazios, valores nulos, strings muito longas)
- Garantir que validações importantes sejam duplicadas no backend (nunca confiar apenas no frontend)
- Diferenciar entre validação no frontend (para UX) e no backend (para segurança). Confirmar que a validação crítica de segurança **sempre** ocorre no backend.

> [!NOTE]
> Entradas não validadas podem causar erros críticos, falhas de segurança ou experiências frustrantes para o usuário — além de abrir portas para ataques de injeção e corrupção de dados.

> 💡 **Exemplo real**: 
> Um banco permitiu que usuários inserissem texto livre em campos numéricos de transferência, resultando em uma transferência acidental de R$10.000.000 em vez de R$10.000,00 (o sistema interpretou a vírgula como separador de milhares). Em outro caso, um sistema de saúde permitiu a entrada de dados sem validação, resultando em prescrições médicas com dosagens incorretas que causaram sérios danos a pacientes quando unidades de medida foram interpretadas de forma ambígua.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Examine todas as funções e rotas que aceitam entrada do usuário. Verifique se
existem validações adequadas (tipo, formato, tamanho) antes do processamento dos
dados. Identifique pontos onde falta validação ou onde entradas maliciosas poderiam
causar comportamentos inesperados. Destaque quais validações são essenciais para a
segurança e devem obrigatoriamente existir no backend, mesmo que já existam no
frontend para melhorar a experiência do usuário. Sugira implementaÇões de validação
robusta para cada campo de entrada.
```

### 16\. Validar autenticação e autorização de usuários

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Garantir que apenas usuários autenticados possam acessar recursos protegidos, e que cada usuário tenha acesso apenas ao que lhe é permitido. A autenticação controla "quem é você", e a autorização determina "o que você pode fazer".

**✅ VERIFICAÇÕES**

- Confirmar que rotas sensíveis exigem autenticação válida
- Verificar que há verificação de permissão para cada ação restrita por perfil
- Avaliar se usuários não conseguem acessar dados de outros apenas modificando parâmetros de URL
- Validar a existência de tokens de autenticação com expiração e renovação segura
- Confirmar que o princípio do menor privilégio está sendo aplicado

> [!NOTE]
> Falhas em autenticação e autorização são causas frequentes de vazamento de dados e violações críticas de segurança. Tais falhas podem ter consequências legais e financeiras severas.

> 💡 **Exemplo real**:
> Uma grande loja virtual sofreu um ataque onde os hackers simplesmente alteraram o ID do usuário na URL (`exemplo.com/perfil/123` para `exemplo.com/perfil/124`) e conseguiram acessar dados de milhões de outros clientes. Em outro caso, uma rede social permitia que usuários comuns acessassem ferramentas administrativas apenas alterando parâmetros no navegador, o que resultou em invasões a contas de celebridades e postagens falsas que chegaram a impactar o mercado financeiro.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Analise o sistema de autenticação e autorização do projeto. Verifique se rotas
sensíveis exigem autenticação e se há verificações para garantir que usuários só
possam acessar recursos permitidos para seu nível de acesso. Identifique endpoints
que possam estar desprotegidos ou onde faltam verificações de permissão. Sugira
melhorias para implementar o princípio de menor privilégio.
```

### 17\. Verificar se há proteção contra ataques comuns

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Prevenir vulnerabilidades clássicas de segurança como injeção de SQL, XSS (Cross-Site Scripting), CSRF (Cross-Site Request Forgery), e a ausência de políticas de segurança como CSP (Content Security Policy), garantindo a integridade e confidencialidade da aplicação e dos dados do usuário.

**✅ VERIFICAÇÕES**

- Confirmar que consultas a banco de dados utilizam ORM ou queries parametrizadas
- Verificar se conteúdos inseridos por usuários são sanitizados antes da renderização
- Avaliar proteção contra XSS (ex: evitar `dangerouslySetInnerHTML`, escapar HTML)
- Garantir uso de tokens CSRF em formulários que alteram dados
- Validar se **headers de segurança HTTP** estão configurados, com destaque para a **CSP (Content Security Policy)**:
    - CSP bloqueia scripts inline e restringe fontes não confiáveis
    - Cabeçalho `Content-Security-Policy` está presente e bem configurado
- Avaliar presença de outros headers de segurança: `X-Content-Type-Options`, `X-Frame-Options`, etc.

> [!NOTE]
> Essas vulnerabilidades continuam entre as mais exploradas na web, mesmo sendo amplamente documentadas. Uma configuração inadequada de headers ou sanitização pode abrir brechas sérias.

> 💡 **Exemplo real**:
> Uma empresa de mídia social teve seu site comprometido por injeção de scripts maliciosos mesmo com outras proteções ativadas. A ausência de CSP permitiu a execução desses scripts, afetando mais de 2 milhões de contas. Uma política CSP adequada teria evitado o ataque.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Examine o código e as configurações da aplicação para identificar
vulnerabilidades comuns:
1) Verifique uso de ORM ou queries parametrizadas contra injeção SQL
2) Avalie sanitização de dados contra XSS
3) Confirme presença de tokens CSRF para formulários e endpoints sensíveis
4) Verifique existência e qualidade da Content Security Policy nos headers HTTP
5) Avalie configuração de outros headers de segurança
Sugira correções conforme diretrizes OWASP.
```

### 18\. Garantir Comunicação Segura com HTTPS

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Proteger os dados dos usuários durante a comunicação com o servidor, impedindo interceptações e adulterações com o uso obrigatório de **HTTPS** e a eliminação de **conteúdo misto**.

**✅ VERIFICAÇÕES**

- Confirmar que todas as comunicações utilizam **HTTPS**
- Verificar se há **redirecionamento automático de HTTP para HTTPS**
- Validar que **nenhum recurso externo (imagens, scripts, APIs)** é carregado via HTTP em páginas HTTPS
- Checar se **certificados SSL** estão válidos e atualizados
- Avaliar se cabeçalhos de segurança estão configurados: `Strict-Transport-Security (HSTS)`, `Content-Security-Policy`, etc.

> [!NOTE]
> Falhas na comunicação segura colocam em risco senhas, dados de pagamento e outras informações sensíveis — especialmente em redes públicas (como WiFi de cafeterias, coworkings, aeroportos).

> 💡 **Exemplo real**:  
> Um site de login usado em cafeterias transmitia dados via HTTP. Em ataques man-in-the-middle, criminosos capturaram senhas de milhares de clientes que estavam no WiFi da loja. Em outro caso, imagens carregadas via HTTP em uma página HTTPS permitiram a injeção de código malicioso para roubar dados de cartão de crédito.

**🤖 Prompt Sugerido para Agente de IA (Claude Code / Cursor / AI Agent)**

```
Analise a configuração do servidor e as URLs no código fonte.  
Verifique se todas as comunicações são forçadas a usar HTTPS com redirecionamentos
adequados de HTTP para HTTPS.  
Identifique recursos (imagens, scripts, APIs) que possam estar sendo carregados
via HTTP em páginas HTTPS, causando avisos de conteúdo misto.  
Confirme se os cabeçalhos de segurança HTTP apropriados estão configurados (HSTS,
Content-Security-Policy).
```

## 📊 Monitoramento e Manutenção

### 19\. Checar presença de logs adequados

**Nível:** 🟡 Intermediário

**🎯 OBJETIVO**

Assegurar que eventos críticos do sistema estejam sendo registrados de forma adequada, sem comprometer informações sensíveis. Logs bem configurados auxiliam no monitoramento, na auditoria e na detecção de falhas ou ataques.

**✅ VERIFICAÇÕES**

- Verificar se a aplicação registra eventos importantes como:
	- Tentativas de login (sucesso e falha)
    - Ações críticas do usuário (ex: exclusão de dados, alterações de perfil)
    - Erros e exceções de execução
- Confirmar que os logs não armazenam informações sensíveis como:
    - Senhas
    - Tokens de autenticação
    - Dados pessoais (ex: CPF, endereço, e-mail) sem anonimização
- Avaliar se os logs são persistentes, acessíveis via ferramenta centralizada (ex: ELK, Datadog, Sentry) e integrados com alertas

> [!NOTE]
> Tanto a ausência quanto o excesso de logs indevidos podem ser desastrosos. Logs insuficientes impedem a investigação de problemas e ataques. Logs mal configurados podem vazar dados sensíveis.

> 💡 **Exemplo real**:
> Uma instituição financeira foi invadida e os hackers permaneceram no sistema por 8 meses sem serem detectados porque não havia logs de acesso adequados. Quando finalmente descobriram a invasão, já era tarde demais. Em outro caso, uma empresa de saúde armazenava senhas e dados médicos completos nos logs, que eram acessíveis para toda a equipe de TI — o que resultou em vazamento, violação da LGPD e multas milionárias.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Analise o sistema de logging da aplicação. Verifique se eventos críticos como
tentativas de login (sucesso/falha), alterações importantes nos dados e erros de
sistema são registrados. Certifique-se que informações sensíveis como senhas,
tokens e dados pessoais não são gravados nos logs. Sugira melhorias para implementar
um sistema de logging abrangente mas seguro.
```

### 20\. Controle de Dependências de Terceiros

**Nível:** 🟡 Intermediário

**🎯 OBJETIVO**

Garantir que bibliotecas e pacotes utilizados na aplicação estejam seguros, atualizados e livres de componentes não destinados à produção. Reduz riscos de segurança, conflitos e problemas de licenciamento.

**✅ VERIFICAÇÕES**

- Verificar se as bibliotecas utilizadas são ativamente mantidas e confiáveis
- Confirmar que não há dependências com vulnerabilidades conhecidas (ex: via `npm audit`, `yarn audit`, `pnpm audit`, `snyk`)
- Validar se bibliotecas desnecessárias, obsoletas ou não utilizadas foram removidas
- Garantir que ferramentas como `dependabot`, `renovate` ou CI com verificação automática estão habilitadas
- Verificar se não há código de demonstração, exemplo ou teste incluído na versão final
- Avaliar se há sobrecarga de dependências para tarefas simples que poderiam ser resolvidas com código nativo

> [!NOTE]
> Ataques via dependências de terceiros são cada vez mais frequentes. Além disso, pacotes abandonados ou inchados aumentam o tempo de build, consumo de memória e risco de falhas.

> 💡 **Exemplo real**:  
> Uma empresa de crédito foi vítima de vazamento de dados de 147 milhões de clientes por não atualizar uma biblioteca Apache Struts com vulnerabilidade conhecida. O impacto do incidente superou US$ 1,4 bilhão.

**🤖 Prompt Sugerido para Agente de IA (Claude Code / Cursor / AI Agent)**

```
Examine o arquivo package.json (ou equivalente) e identifique:
1) Dependências desatualizadas ou com alertas de segurança
2) Bibliotecas com poucos mantenedores ou inativas há muito tempo
3) Código de exemplo ou teste presente na base de produção
4) Bibliotecas usadas para tarefas simples que poderiam ser resolvidas
nativamente
Sugira atualizações, remoções e substituições adequadas.
```

## 🚀 Deploy

### 21\. Armazenamento Seguro e Política de Senhas

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Assegurar que senhas de usuários sejam tratadas com o mais alto nível de segurança possível: desde sua criação até seu armazenamento e recuperação. Boas políticas de senha protegem os usuários e evitam violações catastróficas.

**✅ VERIFICAÇÕES**

- Confirmar que senhas são armazenadas **criptografadas com hash** (ex: `bcrypt`, `argon2`)
- Verificar se o sistema exige **senhas fortes** (mínimo de caracteres, letras, números e símbolos)
- Garantir que **não há senhas em texto puro** armazenadas em banco de dados ou log
- Validar o uso de **salt único por usuário**
- Confirmar que há um **fluxo seguro de redefinição de senha** (tokens temporários, expiração)

> [!NOTE]
> Senhas mal gerenciadas podem comprometer toda a base de usuários. Muitas pessoas reutilizam senhas em múltiplos sistemas, amplificando os riscos em caso de vazamento.

> 💡 **Exemplo real**:  
> Uma rede de hotéis armazenava senhas sem hash adequado. Após uma invasão, os hackers conseguiram acessar dados pessoais e de cartão de crédito de milhões de hóspedes. A empresa foi processada e teve que pagar mais de **US$ 700 milhões** em indenizações.

**🤖 Prompt Sugerido para Agente de IA (Claude Code / Cursor / AI Agent)**

```
Examine o código relacionado ao gerenciamento de senhas.  
Verifique se há validações para senhas fortes (comprimento mínimo, caracteres
especiais, números).  
Confirme que as senhas são armazenadas usando algoritmos de hash modernos como
bcrypt ou Argon2 e nunca em texto plano.  
Verifique também a presença de salt único para cada usuário e se existe um
mecanismo de redefinição de senha seguro.
```

### 22. Preparação para Produção

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Assegurar que a aplicação esteja pronta para ser executada em ambiente de produção, com todas as configurações otimizadas, variáveis corretamente definidas, e sem dependências ou práticas de desenvolvimento ativas. Isso reduz riscos de falhas, vazamentos e problemas de performance após o deploy.

**✅ VERIFICAÇÕES**

- Confirmar que `NODE_ENV` está definido como `'production'`
- Verificar que todas as variáveis de ambiente sensíveis estão configuradas e carregadas corretamente
- Validar que endpoints e URLs usados (APIs, bancos de dados, CDNs) apontam para os serviços de produção
- Checar que não há configurações de debug ou logs verbosos habilitados
- Confirmar que o build está otimizado (minificado, sem source maps abertos)
- Avaliar se o processo de build inclui code splitting, cache busting e compressão (ex: gzip, brotli)

> [!NOTE]  
> Pequenos descuidos em configurações de produção podem levar a impactos graves, como lentidão generalizada, quebra de funcionalidades ou até vazamento de dados.

> 💡 **Exemplo real**:  
> Uma empresa SaaS esqueceu de definir `NODE_ENV` como `'production'`, o que fez com que todo o React rodasse em modo de desenvolvimento — gerando mensagens de console desnecessárias, builds não otimizados e desempenho 50% inferior. O erro foi detectado só após o aumento de churn de clientes causado por lentidão nas telas.

**🤖 PROMPT PARA CURSOR / CLAUDE CODE / AI Agent**

```
Verifique preparação para produção:

1. CONFIGURAÇÕES:
   - Confirme que NODE_ENV está definido como 'production'
   - Verifique se URLs de API, banco de dados e storage apontam para os
ambientes corretos
   - Identifique flags de debug, logs verbosos ou configurações de
desenvolvimento ativas

2. OTIMIZAÇÕES:
   - Confirme que o build está minificado e com code splitting
   - Verifique se source maps estão desativados ou ofuscados
   - Avalie se há uso de compressão (gzip, brotli) e cache headers

3. VARIÁVEIS DE AMBIENTE:
   - Confirme que todas as variáveis obrigatórias estão definidas
   - Valide que não há variáveis sensíveis hardcoded no código fonte
   - Sugira checklist automatizado de validação em CI para ambientes
```

## 🤖 Uso Crítico da IA

### 23\. IA no Loop: Validação Crítica de Sugestões

**Nível:** 🟢 Fundamental

**🎯 OBJETIVO**

Estimular o pensamento crítico na adoção de sugestões geradas por agentes de IA, garantindo que todo código aceito passe por revisão humana consciente. A IA deve acelerar o trabalho, mas não substituir o julgamento técnico responsável.

**✅ VERIFICAÇÕES**

- Confirmar que os desenvolvedores compreendem o código sugerido pela IA antes de aceitá-lo
- Verificar se sugestões de IA seguem os padrões de estilo e arquitetura do projeto
- Avaliar se os efeitos colaterais de trechos gerados foram considerados (ex: async/await fora de função, dependências omitidas, lógica fora de contexto)
- Incentivar o uso de revisão por pares mesmo em código originado por IA

> [!NOTE]
> Aceitar código gerado por IA sem análise crítica pode introduzir bugs silenciosos, violar boas práticas do projeto e causar falhas em produção.

> 💡 **Exemplo real**:  
> Em uma empresa de logística, a sugestão de IA foi aceita sem revisão e introduziu um `await` fora de uma função `async`, quebrando a build. O erro só foi percebido após o deploy, derrubando o serviço por horas. Desde então, a empresa adotou a regra: "IA sugere, humano valida."

**🤖 Prompt Sugerido para Agente de IA (Claude Code / Cursor / AI Agent)**

```
Revise criticamente este trecho sugerido por IA.  
1) Qual é o propósito da sugestão?  
2) O código gerado segue o estilo do time e as boas práticas do projeto?  
3) Há riscos ocultos, como dependências implícitas, comportamentos assíncronos
mal definidos ou acoplamento?  
Sugira modificações para que o código esteja de fato alinhado com os padrões
da equipe.
```

## Estratégia Implementada: Combinação de 2 LLMs para Melhoria da Segurança

### Objetivo
O código implementa uma estratégia de segurança ao combinar dois Modelos de Linguagem Natural (LLMs) para detectar e bloquear prompts maliciosos ou potencialmente perigosos. Essa abordagem envolve a utilização de um LLM especializado em classificação de prompts jailbreak e um segundo LLM para gerar respostas seguras a partir dos prompts considerados seguros.

### Como Funciona a Combinação de LLMs
1. **LLM de Detecção de Jailbreak:**
   - O primeiro LLM é responsável por classificar os prompts recebidos e detectar possíveis tentativas de jailbreak, onde o usuário tenta contornar restrições e instruções pré-definidas.
   - Esse modelo utiliza uma lista de palavras-chave perigosas e padrões conhecidos de jailbreak para identificar prompts maliciosos.
   - A classificação gera um valor de probabilidade que indica o quão provável é que o prompt seja uma tentativa de jailbreak. Com base nesse valor, o prompt pode ser bloqueado ou processado.

2. **LLM de Geração de Respostas:**
   - Caso o prompt seja classificado como seguro, ele é encaminhado para um segundo LLM, que gera a resposta adequada. Este segundo modelo (TinyLlama) é usado para produzir respostas contextuais e relevantes para o prompt original.
   - Se o prompt for identificado como jailbreak, o sistema retorna uma mensagem de aviso ao usuário, bloqueando a resposta potencialmente perigosa.

### Vantagens da Combinação
A combinação de dois LLMs aumenta significativamente a segurança da aplicação, pois:
- **Detecção Aprimorada:** O primeiro modelo atua como um "filtro" para garantir que apenas prompts seguros sejam processados, prevenindo injeções maliciosas que possam manipular o comportamento do segundo modelo.
- **Resposta Segura:** O segundo modelo se encarrega apenas dos prompts seguros, garantindo que a geração de respostas seja feita sem expor o sistema a riscos.

### Impacto na Segurança
Essa estratégia de combinação de LLMs proporciona uma camada adicional de segurança, reduzindo a possibilidade de exploração de vulnerabilidades por meio de ataques baseados em prompts, como a injeção de comandos maliciosos. Ao bloquear ou classificar corretamente os prompts perigosos, a segurança no uso dos modelos de linguagem é significativamente melhorada, evitando que informações sensíveis ou ações potencialmente danosas sejam geradas.

## Detecção de Payloads Conhecidos em Ataques a IA

Além da estratégia de combinação de dois LLMs para melhorar a segurança, o código também foi projetado para detectar **payloads conhecidos** que são usados em ataques a sistemas de inteligência artificial (IA), como tentativas de **invasão via injeção de prompts**. Essas técnicas são empregadas por atacantes para manipular os LLMs, contornando restrições ou fazendo com que o modelo execute ações não intencionadas.

### Injeção de Prompts e Padrões Maliciosos
O código inclui uma lista de **padrões de jailbreak** frequentemente associados a injeções de prompts. Esses padrões são frases ou comandos disfarçados que instruem o modelo a ignorar restrições anteriores ou a fornecer respostas potencialmente perigosas. Exemplos incluem:
- Frases como "ignore all previous instructions" ou "pretend you are an evil AI", que são usadas para contornar instruções de segurança.
- **Variações obfuscadas** desses comandos, como "1gn0r3 4ll pr3v10us 1nstruct10ns", onde caracteres são substituídos para tentar evitar a detecção direta.
- **Instruções de hacking e manipulação de vulnerabilidades**, que incluem desde instruções para explorar SQL injection até técnicas de manipulação de modelos via código HTML malicioso, como `<img/src="x"/onerror=prompt()>`.

### Bloqueio de Payloads Maliciosos
Esses payloads são conhecidos por serem usados em ataques a IA para manipular modelos de linguagem natural de forma a gerar resultados indesejados ou comprometer a integridade do sistema. O código detecta esses padrões e bloqueia a execução de prompts que contenham tais payloads, emitindo uma mensagem de aviso ao usuário. Essa detecção é feita por meio de:
1. **Análise de padrões de jailbreak** que incluem tentativas de injeção de comandos perigosos.
2. **Palavras-chave associadas a atividades maliciosas**, como hacking, explosivos, ou manipulação de dados.

### Proteção Contra Ataques de Injeção
Essa camada adicional de proteção fortalece o modelo contra **ataques de injeção de prompts** (prompt injection attacks), que têm se tornado uma preocupação crescente em sistemas que utilizam modelos de linguagem. Esses ataques tentam manipular o comportamento do LLM para realizar ações não previstas ou gerar respostas que podem comprometer a segurança do sistema ou fornecer informações sensíveis. Ao identificar e bloquear esses ataques, o código protege contra tentativas de exploração maliciosa.

### Conclusão
Ao combinar dois LLMs e incluir mecanismos de detecção de payloads conhecidos e padrões maliciosos, o código não só melhora a segurança no uso do modelo de linguagem, mas também fortalece a defesa contra **ataques de injeção** e **manipulações maliciosas**. Essa abordagem é essencial para garantir que o sistema permaneça seguro e confiável, mesmo diante de tentativas avançadas de exploração.

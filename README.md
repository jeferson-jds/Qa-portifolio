# Meu Mapa QA — Jeferson da Silva

Este repositório documenta minha jornada de transição e evolução técnica na área de Quality Assurance (QA), estruturada através do método de prática e aplicação real.

---

## 📋 Sumário
- [Semana 1 — Minha base em QA](#semana-1--minha-base-em-qa)
- [Semana 2 — Técnicas de Teste na Prática](#semana-2--técnicas-de-teste-na-prática)
- [Semana 3 e 4 — Planejamento e Casos de Teste (BugBank)](#semana-3-e-4)
- [Semana 5 e 6 — Execução Avançada e Relatório de Testes](#semana-5-6)

---

## Semana 1 — Minha base em QA

**Foco:** Nivelamento — construir a base conceitual do QA para entrar nos próximos encontros com segurança, sem lacunas.

### Os conceitos de hoje, com minhas palavras
* **O que é software, pra mim:** Software é um sistema construído através de uma linguagem de programação para resolver uma necessidade ou uma dor.
* **O que é qualidade de software, pra mim:** Qualidade de software é quando o software atende aos requisitos e as regras de negócio aos quais foram especificados, entregando o que foi esperado pelo usuário com confiabilidade, usabilidade e segurança.
* 
* **O papel do QA — técnico e comportamental:** O QA deve entender os requisitos, fazer um bom planejamento dos testes, executar os testes, registrar os erros encontrados e acompanhar esses erros até a resolução. No comportamento, o QA precisa ter resiliência, proatividade e senso crítico. Não deve confiar em uma informação, mas sempre verificar e buscar evidências reais.
* 
* **Os dois princípios de teste:** 
  * *Testes exaustivos são impossíveis:* Existem muitas combinações e possibilidades, cenários diversos, então não é possível testar tudo. Por isso, precisamos direcionar os testes para os pontos de maior risco e importância.
  * 
  * *Teste depende de contexto:* A estratégia muda conforme o produto, o contexto dita a prioridade, o usuário e o risco envolvido (ex: um sistema médico foca em precisão de dados e segurança; um app de entrega foca em usabilidade e agilidade).
* **O processo de teste, em poucas palavras:** Entender os requisitos, planejar os testes, executar, registrar o que encontrou, acompanhar os erros até resolver e verificar que o que foi alterado não quebrou o que já estava em bom funcionamento.

### Meu app em análise (Site da Netshoes)
| Ponto observado | O que percebi e por quê |
| :--- | :--- |
| **Uma função de boa qualidade** | Gostei do site, a heurística visual é atrativa, possui boa acessibilidade até para pessoas com deficiência, atendimento em libras e achei rápido. |
| **Uma função de qualidade ruim** | Ao buscar por "blusa lacoste", a listagem retorna itens divergentes, como calçados (Chinelos e Tênis Lacoste), prejudicando a precisão da pesquisa. Não impede a compra, mas é uma indexação incorreta de palavras-chave. |
| **O que um QA investigaria aqui** | Divergências nas pesquisas e paginação avançada (ex: página 60 exibindo itens incorretos). O usuário pode não se importar tanto, mas é um desalinhamento técnico. |

### Por que qualidade de software importa
> **Minha frase-síntese:** "Qualidade de software vai muito além de encontrar bugs: é uma necessidade estratégica que reduz custos com retrabalho, otimiza o tempo de entrega da equipe e protege a credibilidade do produto no mercado através de clareza e evidências."

---

## Semana 2 — Técnicas de Teste na Prática

Nesta semana, dei o primeiro passo da teoria para a prática: aprendi três técnicas de design de teste (Partição de Equivalência, Valor Limite e Tabela de Decisão) e apliquei cada uma delas sobre regras de negócio reais.

### As técnicas que aprendi
* **Partição de Equivalência:** Divide os dados de entrada em grupos válidos e inválidos. Agrupa dados por comportamento e testa um representante de cada grupo.
* **Valor Limite:** Técnica usada para testar as bordas de uma partição, ou seja, os valores que ficam nos limites onde uma regra pode mudar de comportamento. Existe porque os erros costumam se concentrar justamente nas bordas.
* **Tabela de Decisão:** Analisa a lógica e combinações de múltiplas regras e condições.

### Regras de Negócio Trabalhadas
1. **Cupom de desconto:** Guia a criação dos casos de teste analisando as regras de entrada.
2. **Frete grátis:** Conjunto de condições que verifica critérios para autorizar ou negar o desconto do frete.

### Casos de Teste — Cupom de Desconteo / Frete
| # | Cenário testado | Valor / Data de entrada | Resultado esperado | Partição ou Limite? |
| :-: | :--- | :--- | :--- | :--- |
| 1 | Validar frete no limite mínimo | 200 | Frete grátis | Valor limite - válido |
| 2 | Validar frete 1 centavo abaixo do limite mínimo | 199,99 | Frete cobrado | Valor limite - inválido |
| 3 | Validar frete com valor acima do limite | 200,01 | Frete grátis | Partição de equivalência |
| 4 | Validar frete para cliente prime abaixo do limite | 50 | Frete grátis | Partição de equivalência válida |
| 5 | Validar frete para cliente não prime abaixo do limite | 100 | Frete cobrado | Partição de equivalência inválida |
| 6 | Validar compra com CEP fora da área | 250 (CEP fora de área) | Compra bloqueada | Partição inválida |

### Tabela de Decisão — Frete Grátis
| # | CEP fora da área? | Valor ≥ R$ 200? | Cliente Prime? | Resultado esperado |
| :-: | :-: | :-: | :-: | :--- |
| 1 | Sim | Sim | Sim | Compra bloqueada |
| 2 | Não | Sim | Não | Frete grátis |
| 3 | Não | Não | Sim | Frete grátis |
| 4 | Sim | Não | Não | Compra bloqueada |

---

## Semana 3 e 4

Foco na aplicação prática sobre o [BugBank](https://bugbank.netlify.app/).

### Casos de Teste — Cadastro (Exemplos)

#### ID: CT-001
* **Título:** Tentativa de cadastro sem preencher senha deve visualizar a mensagem "Senha não pode ser vazio"
* **Prioridade:** Alta
* **Pré-condição:** Estar na tela de cadastro.
* **Passos:** Acessar tela -> Preencher e-mail (`Qateste_cs@gmail.com`) -> Preencher nome -> Deixar senha vazia -> Clicar em "Cadastrar".
* **Resultado Esperado:** Mensagem "Senha não pode ser vazio".
* **Resultado Encontrado:** "Campo obrigatório." *(Divergência identificada)*
* **Gherkin:**
  ```gherkin
  Cenário: Tentativa de cadastro sem preencher a senha
    Dado que estou na tela de cadastro
    E informo o e-mail "Qateste_cs@gmail.com"
    E informo um nome válido
    E deixo o campo senha vazio
    Quando clico no botão "Cadastrar"
    Então o sistema deve impedir o cadastro
    E devo visualizar a mensagem "Senha não pode ser vazio"

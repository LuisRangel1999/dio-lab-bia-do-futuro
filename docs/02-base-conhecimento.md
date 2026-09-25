# Base de Conhecimento

## Dados Utilizados


| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `conceitos_cripto.json` | JSON | Armazenar definições e explicações de conceitos fundamentais de criptomoedas, blockchain, carteiras, chaves, mineração, staking e taxas de rede. |
| `criptoativos.json` | JSON | Apresentar características básicas de Bitcoin, Ether, stablecoins e tokens, sem definir qual ativo deve ser comprado. |
| `riscos_cripto.json` | JSON | Orientar explicações sobre volatilidade, golpes, custódia, transações, contratos inteligentes e riscos regulatórios. |
| `faq_cripto.csv` | CSV | Fornecer respostas-base para dúvidas frequentes e manter maior consistência nas explicações. |
| `fontes_confiaveis.json` | JSON | Registrar fontes utilizadas para construir e verificar a base de conhecimento. |
| `perfil_usuario.json` | JSON | Personalizar o nível de profundidade e a linguagem das explicações de acordo com o conhecimento e os interesses do usuário. |
| `historico_atendimento.csv` | CSV | Manter o contexto de interações anteriores e identificar assuntos já explicados ao usuário. |

### Fonte dos dados

As informações utilizadas para construir e verificar a base de conhecimento foram obtidas a partir de fontes institucionais e de documentação técnica reconhecida sobre o tema:

- [Banco Central do Brasil (BCB)](https://www.bcb.gov.br/meubc/faqs/s/moedas-virtuais) — definições de ativos virtuais, informações sobre regulação brasileira e riscos relacionados ao tema.
- [Comissão de Valores Mobiliários (CVM)](https://www.gov.br/cvm/pt-br/assuntos/protecao/mercado-forex) — informações sobre riscos, fraudes, volatilidade e enquadramento de determinados criptoativos no mercado de valores mobiliários.
- [Bitcoin.org](https://bitcoin.org/en/how-it-works) — funcionamento do Bitcoin, blockchain, transações, chaves e mineração.
- [Bitcoin Whitepaper](https://bitcoin.org/pt_BR/bitcoin-paper) — documento original que descreve o funcionamento do protocolo Bitcoin.
- [Ethereum.org](https://ethereum.org/pt-br/what-is-ethereum/) — Ethereum, Ether, carteiras, contas, chaves, gas e contratos inteligentes.

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Os dados mockados originais foram substituídos por uma base de conhecimento específica para o contexto de criptomoedas. Foram criados arquivos com conceitos fundamentais, características de diferentes categorias de criptoativos, riscos e segurança, perguntas frequentes, fontes confiáveis e dados de contexto do usuário. O conteúdo foi estruturado com foco educativo, sem preços, previsões de mercado ou recomendações de investimento, para reduzir a dependência de informações que mudam rapidamente e manter o agente alinhado ao seu propósito.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Os arquivos JSON e CSV da pasta `data` são carregados pela aplicação durante a inicialização e armazenados em estruturas de dados Python. Os arquivos `conceitos_cripto.json`, `criptoativos.json`, `riscos_cripto.json` e `fontes_confiaveis.json` armazenam informações sobre criptomoedas, enquanto o `perfil_usuario.json` fornece informações para contextualizar o usuário e o `historico_atendimento.csv` registra interações anteriores. `O faq_cripto.csv` contém perguntas e respostas-base para auxiliar na geração das respostas do agente.

```python
# ============ CARREGAR DADOS ============
perfil = json.load(open('./data/perfil_usuario.json'))
conceitos = json.load(open('./data/conceitos_cripto.json'))
criptoativos = json.load(open('./data/criptoativos.json'))
riscos = json.load(open('./data/riscos_cripto.json'))
fontes = json.load(open('./data/fontes_confiaveis.json'))
faq = pd.read_csv('./data/faq_cripto.csv')
historico = pd.read_csv('./data/historico_atendimento.csv')

````

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Os dados não serão colocados integralmente no system prompt. O system prompt definirá as regras gerais de comportamento do Theo, enquanto a aplicação selecionará dinamicamente os trechos relevantes da base de conhecimento e os adicionará ao contexto da solicitação. O contexto da conversa também será considerado para que perguntas de continuidade possam ser respondidas com maior precisão. Quando a informação necessária não estiver na base de conhecimento nem no contexto disponível, o agente deverá declarar a limitação em vez de inventar uma resposta.

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Perfil do Usuário:
- Nome: Marina
- Nível de conhecimento: Iniciante
- Objetivo: Aprender os fundamentos de criptomoedas
- Preferência: Explicações didáticas com analogias simples

Contexto da Conversa:
- Usuária perguntou anteriormente sobre a diferença entre Bitcoin e blockchain.
- Agora perguntou: "O que é uma carteira de criptomoedas?"

Dados da Base de Conhecimento:
- Conceito: Carteira (wallet)
- Definição: Aplicação ou dispositivo usado para acessar contas, visualizar saldos e assinar transações com ativos digitais.
- Explicação para iniciantes: A carteira permite controlar as chaves usadas para acessar os ativos registrados na blockchain.
- Fonte: Ethereum.org

Regras de Resposta:
- Explicar de forma acessível e didática.
- Usar uma analogia simples quando ajudar na compreensão.
- Não recomendar compra ou venda de ativos.
- Não inventar informações ausentes da base ou do contexto.
```

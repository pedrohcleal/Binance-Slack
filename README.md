# TradingBotPy

# Binance Trading Bot

Este é um arquivo Python que implementa um bot de negociação para a plataforma de criptomoedas Binance. O bot utiliza a biblioteca `websocket` para se conectar ao fluxo de dados em tempo real da Binance e executa negociações com base na estratégia do Índice de Força Relativa (RSI). O arquivo é um script Python autônomo que pode ser executado para automatizar as negociações em um par de criptomoedas específico (neste caso, BNBBUSD).

Aqui está uma explicação das partes essenciais do código:

1. **Importações de bibliotecas:**
   - `json`: Usada para analisar mensagens JSON recebidas pelo WebSocket.
   - `websocket`: Usada para estabelecer uma conexão WebSocket com a Binance.
   - `pprint`: Usada para imprimir mensagens de depuração de forma legível.
   - `talib`: Biblioteca TA-Lib (Análise Técnica) usada para calcular o Índice de Força Relativa (RSI).
   - `numpy`: Usada para trabalhar com matrizes de preços de fechamento.
   - `config`: Presumivelmente, um arquivo de configuração contendo as credenciais da API da Binance.

2. **Constantes e Variáveis:**
   - `SOCKET`: O URL do WebSocket da Binance para o par de negociação BNBBUSD no intervalo de 1 minuto.
   - `RSI_PERIOD`: O período usado para calcular o RSI.
   - `RSI_OVERRBOUGHT`: O limite superior do RSI que indica um mercado sobrecomprado.
   - `RSI_OVERSOLD`: O limite inferior do RSI que indica um mercado sobrevendido.
   - `TRADE_SYMBOL`: O par de negociação que o bot irá negociar (BNBBUSD).
   - `TRADE_QUANTITY`: A quantidade de ativos que o bot comprará ou venderá em cada negociação.
   - `closes`: Uma lista que armazena os preços de fechamento das velas.
   - `in_position`: Uma variável booleana que rastreia se o bot está atualmente em uma posição (comprado) ou não.
   - `ultimo_preco`: O preço da última vela, usado para rastrear a última execução de negociação.

3. **Funções:**
   - `order`: Uma função que envia uma ordem de negociação para a Binance com base nas informações fornecidas, como lado (compra/venda), quantidade e tipo de ordem.
   - `on_open`, `on_close`, `on_message`: Funções de retorno de chamada para lidar com eventos relacionados à conexão WebSocket, como abertura, fechamento e recebimento de mensagens.

4. **Lógica Principal:**
   - A função `on_message` é chamada sempre que uma nova mensagem é recebida do fluxo de dados em tempo real. Ela processa os dados da vela e calcula o RSI com base nas velas fechadas anteriores.
   - Com base no valor do RSI, o bot decide se deve comprar, vender ou não fazer nada. Ele implementa uma estratégia simples de compra quando o RSI está abaixo de um limite inferior e vende quando o RSI está acima de um limite superior.
   - A função `order` é usada para enviar ordens de compra ou venda para a Binance.
   - A lógica geral é automatizar negociações com base em sinais do indicador RSI.

5. **Inicialização do WebSocket:**
   - O código finaliza criando uma instância do WebSocketApp usando o URL do WebSocket da Binance e configurando as funções de retorno de chamada. Em seguida, inicia a conexão WebSocket e entra em um loop infinito para manter a conexão ativa e continuar monitorando o fluxo de dados em tempo real.

**Nota:** Este é um exemplo de código que requer configuração adicional, incluindo chaves de API válidas e parâmetros de negociação, e não deve ser executado sem entendimento e considerações adequadas de risco. A negociação de criptomoedas é arriscada e pode resultar em perdas substanciais.

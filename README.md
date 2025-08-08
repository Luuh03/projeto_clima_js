# Temperatura por cidade (Open‑Meteo)

Aplicativo web simples (HTML + JS) que permite digitar o nome de uma cidade, faz geocodificação via Open‑Meteo para obter latitude/longitude e busca a temperatura atual. Não requer chave de API.

- Tecnologias: HTML, CSS, JavaScript (fetch API)
- APIs: 
  - Geocodificação: https://open-meteo.com/en/docs/geocoding-api
  - Previsão: https://open-meteo.com/en/docs

## Visão geral

O app possui:
- Um campo de entrada para a cidade
- Validação básica (impede busca vazia)
- Chamada à API de geocodificação do Open‑Meteo para obter coordenadas (latitude/longitude)
- Chamada à API de previsão do Open‑Meteo para obter a temperatura atual (°C)
- Mensagens amigáveis de status e erro
- Log do resultado no console do navegador


## Estrutura do projeto

- public/
  - index.html (todo o app)

## Pré-requisitos

- Navegador moderno com suporte a fetch (Chrome, Firefox, Edge, Safari atuais)
- Conexão com a internet

## Instalação e execução

Você pode abrir o arquivo diretamente ou servi-lo com um servidor estático.

Opção A — Abrir diretamente:
1. Clique duas vezes em public/index.html para abrir no navegador.
2. Se o navegador bloquear algumas requisições quando aberto via file://, use a Opção B.

Opção B — Servir estaticamente (recomendado):
- Usando Node.js:
  - npx serve public
- Usando Python 3:
  - cd public
  - python -m http.server 5173
  - Abra http://localhost:5173 no navegador.

## Guia de uso

1. Abra a página do app.
2. Digite o nome da cidade (ex.: “São Paulo”, “Paris”, “Lisboa”).
3. Clique em “Buscar”.
4. Aguarde a mensagem de status:
   - Sucesso: “Temperatura atual em {Cidade, País}: {valor} °C”
   - Cidade não encontrada: mensagem informativa
   - Erro de rede/API: mensagem de erro com sugestão para tentar novamente

Dica: abra o console do navegador (F12) para ver o log com a mesma mensagem.

## Exemplo de resultado

- Entrada:
  - Cidade: São Paulo
- Saída mostrada na tela:
  - “Temperatura atual em São Paulo, Brasil: 23.4 °C”
- Log no console:
  - Temperatura atual em São Paulo, Brasil: 23.4 °C

(Os valores numéricos variam conforme o momento da consulta.)

## Funcionalidades

- Validação de entrada (impede submissão vazia)
- Geocodificação da cidade com parâmetros:
  - name: nome da cidade digitado
  - count=1: pega o melhor resultado
  - language=pt: resultados em português quando disponíveis
  - format=json
- Busca de clima atual com parâmetros:
  - latitude e longitude vindos da geocodificação
  - current_weather=true: retorna temperatura atual
  - timezone=auto: ajusta automaticamente
- Exibição do resultado em texto simples e registro no console
- Mensagens de erro:
  - Cidade não encontrada
  - Falhas HTTP/JSON
  - Problemas de rede
- Acessibilidade básica:
  - aria-label no input
  - role="status" para a área de resultado

## Erros comuns e soluções

- Cidade não encontrada:
  - Tente incluir país/estado (ex.: “Paris, FR”)

- Erro de rede/HTTP:
  - Verifique sua conexão e tente novamente
  - Se estiver abrindo via file:// e houver problemas, sirva a pasta public com um servidor estático

- Temperatura ausente:
  - O endpoint deve retornar current_weather.temperature; tente novamente ou teste com outra cidade
## Personalização
- Idioma dos resultados de geocodificação:
  - Ajuste geoUrl.searchParams.set('language', 'pt') para outro idioma

- Unidade de temperatura:
  - O endpoint atual retorna °C por padrão com current_weather; para garantir, adicione temperature_unit=celsius

- Aparência:
  - Ajuste o CSS embutido conforme necessário

## Melhorias futuras

- Troca de unidades (°C/°F)
- Exibir mais dados: vento, umidade, sensação térmica
- Histórico de buscas e caching em localStorage
- Indicador de carregamento (spinner) e estados de erro mais detalhados
- Testes automatizados (Jest/Vitest) para funções de busca/parsing
- TypeScript e separação do código em módulos
- PWA (offline básico) e deploy em hospedagem estática
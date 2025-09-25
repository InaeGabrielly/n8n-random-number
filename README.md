\# 🎲 Projeto: Integração com Random.org via n8n

Este projeto automatiza a geração de números aleatórios usando a API pública do [Random.org](https://www.random.org), integrado ao workflow do [n8n](https://n8n.io).

O número gerado é tratado e retornado via Webhook, podendo ser usado em aplicações externas, validações ou testes dinâmicos.

\---

\## 🚀 Funcionalidades

- Requisição HTTP para Random.org
- Tratamento da resposta (limpeza de texto e conversão para número)
- Retorno via Webhook com estrutura JSON
- Pronto para deploy via Docker
- Repositório versionado com GitHub
- Suporte a pacotes auxiliares via npm (se necessário)

\---

\## 🧩 Estrutura do Workflow

1. \*Webhook Node\*

Recebe a chamada externa e inicia o fluxo.

1. \*HTTP Request Node\*

Faz uma requisição GET para a URL:

https://www.random.org/integers/?num=1&min=1&max=608&col=1&base=10&format=plain&rnd=new


1. \*Set Node\*

Limpa o valor retornado (\n) e converte para número:

\```n8n

{{ $json["body"].trim() }}



1. Run Once for All Items (JavaScript) Código para garantir que o valor seja limpo e convertido corretamente:

const resposta = $node["HTTP Request"].json["body"];

const numero = (resposta ?? "").toString().trim();

return [

{

json: {

data: parseInt(numero),

fonte: "random.org"

}

}

];


1. Respond to Webhook Node Retorna o número gerado em formato JSON:

{

"data": 55,

"fonte": "random.org"

}




Como rodar com Docker


\# Clone o repositório

git clone https://github.com/seu-usuario/n8n-random-org.git

cd n8n-random-org

\# Suba o container

docker-compose up -d





Instalação de pacotes via npm

Se você estiver usando funções customizadas ou scripts externos:

\# Instale dependências

npm install

\# Execute scripts auxiliares

node scripts/validaNumero.js

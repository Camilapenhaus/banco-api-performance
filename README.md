
Testes de Performance da API do Banco com K6

Repositório com testes de performance automatizados para a API do sistema bancário. Os testes simulam diferentes cargas e cenários de uso para avaliar o desempenho da API e identificar possíveis gargalos. Os scripts são escritos em JavaScript com K6, com foco em modularidade, organização e reutilização de dados e funções.
Repositório: banco-api-performance

Tecnologias utilizadas

K6 — ferramenta open source para testes de carga e performance.
JavaScript (ES6) — linguagem usada nos scripts de teste.
Git e GitHub — versionamento e hospedagem do projeto.
Estrutura do repositório
banco-api-performance/
├── config/
│   └── config.local.json
├── fixtures/
│   └── postLogin.json
├── helpers/
│   └── autenticacao.js
├── tests/
│   ├── login.test.js
│   └── transferencias.test.js
├── utils/
│   └── variaveis.js
├── .gitignore
├── README.md
└── relatorio.html

Objetivo das pastas e arquivos

config/: guarda configurações locais, como a URL base da API.
fixtures/: guarda dados de entrada reutilizados pelos testes, como o corpo da requisição de login.
helpers/: contém funções auxiliares reutilizáveis, como a obtenção do token de autenticação.
tests/: contém os scripts de teste da API, organizados por funcionalidade.
utils/: contém utilitários compartilhados, como a função que obtém a URL base.
relatorio.html: relatório HTML exportado de uma execução do K6.

Instalação e execução

1. Instale o K6
No macOS com Homebrew:
brew install k6
Confira a instalação:
k6 --version
2. Clone o repositório
git clone https://github.com/Camilapenhaus/banco-api-performance.git
cd banco-api-performance
3. Configure a URL da API
Edite config/config.local.json e informe a URL base da API. Para o ambiente local:
{
  "baseURL": "http://localhost:3000"
}
Os scripts podem usar a variável de ambiente BASE_URL quando ela for informada. Se ela não for passada, o utilitário do projeto usa a URL definida no arquivo local de configuração.
4. Execute os testes
Login:
k6 run tests/login.test.js
Transferência:
k6 run tests/transferencias.test.js
Para informar a URL pela linha de comando, use -e antes do caminho do script:
k6 run -e BASE_URL=http://localhost:3000 tests/login.test.js
5. Acompanhe o teste em tempo real e exporte o relatório
O comando abaixo abre o dashboard do K6 durante a execução e salva o relatório HTML como html-report.html ao final:
K6_WEB_DASHBOARD=true \
K6_WEB_DASHBOARD_EXPORT=html-report.html \
k6 run -e BASE_URL=http://localhost:3000 tests/login.test.js
O relatório será criado na pasta do projeto. Para gerar o relatório durante um teste de transferência, substitua tests/login.test.js por tests/transferencias.test.js.


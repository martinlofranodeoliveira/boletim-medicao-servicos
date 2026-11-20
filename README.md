# Boletim de Medição de Serviços

Simule ocorrências fictícias e confira como faixas de pontos alteram o valor do boletim.

## Como usar

Abra a [demonstração](https://martinlofranodeoliveira.github.io/boletim-medicao-servicos/). Para uso local, execute `python3 -m http.server 8000` no diretório e abra `http://localhost:8000`.

Informe grossCents, bands com minPoints e rateBps, e events com id e points. Um rateBps de 300 significa 3%.

## Contrato público

input deve ser objeto com grossCents (inteiro de 0 a 100000000), bands (array de até 20 {minPoints,rateBps}) e events (array de até 100 {id,points}). points e minPoints são inteiros de 1 a 10000. minPoints aumenta estritamente, e rateBps é inteiro de 0 a 10000 e não diminui entre faixas. id tem 1 a 32 caracteres ASCII alfanuméricos, hífen ou sublinhado e é único em events. Entrada inválida retorna exatamente {error:"INVALID_INPUT"}.
Retorne {rows,summary}. Some points na ordem dos eventos. Em cada evento escolha a taxa da última faixa com minPoints menor ou igual aos pontos acumulados (0 quando nenhuma se aplica). Arredonde grossCents*rateBps/10000 a centavos inteiros com meio para cima. A linha {id,cumulativePoints,rateBps,discountCents} registra em discountCents somente a diferença entre o desconto acumulado atual e o do evento anterior. summary tem grossCents, discountCents (todo o desconto) e netCents (bruto menos desconto).

## Escopo

Demonstração offline com exemplos fictícios. A equipe responsável avalia documentação, conformidade e habilitação. A interface processa os dados no navegador. O motor foi gerado com Gemini 4 Neon no Vertex AI.

## Testes

Execute `node scripts/test.mjs public.json`.

## Licença

MIT. Acorn preserva sua licença em scripts/vendor/LICENSE-Acorn.txt.

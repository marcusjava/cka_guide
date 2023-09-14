###Por que usar JSON Path com utilitario kubectl?

- Capacidade de manipular um grande numero de datasets(+100 nodes, +1000 pods, deployments, replicasets)
- Possui filtro avançado para melhor exibição dos resultados

###Como utilizar JSON Path?

Para começar a utilizar JSON path com kubectl é necessario estar bem familiarizado com o formato JSON, com json path é possivel criar queries complexas e formatar os dados para exibição. Recurso muito util quando temos arquivos JSON grandes e complexos.

- Exibir informações no formato JSON
  `kubectl get nodes -o json `
- Copiar a saída e criar as queries. Uma dica é utilizar o site http://jsonpath.com/
- Usar jsonpath como output para exibir somente as informações desejadas
  `kubectl get pod nginx -o jsonpath='{.items[].spec.containers[0].image}'`

### Loops - Range

Recurso interessante que permite iterar sobre listas

`get nodes -o jsonpath='{range .items[*]} {.metadata.name} {" - "} {.status.capacity.cpu} {"\n"} {end}' `

### Custom columns

Para definir custom columns e exibir somente os detalhes em uma tabela podemos usar

`kubectl get nodes -o custom-columns=NODE:.metadata.name,CPU:.status.capacity.cpu `

### Sort columns

###Exemplos

Exibindo info sobre taints no node
`kubectl get node kind-control-plane -o jsonpath='{.metadata.name} {"\n"} { .spec.taints }' `

Exibindo info sobe a CPU em todos os nodes

`kubectl get nodes -o jsonpath='{.items[*].metadata.name} {"\n"} { .items[*].status.capacity.cpu }  '`

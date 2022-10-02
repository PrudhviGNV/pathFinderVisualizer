# PathFinding-Visualizer: - UMA APLICAÇÃO FEITA COM REACT
 [![NodeJS](https://img.shields.io/badge/node-12.14.1-important)](https://img.shields.io/badge/node-12.14.1-important)
 [![NPM](https://img.shields.io/badge/npm-6.13.7-blueviolet)](https://img.shields.io/badge/npm-6.13.7-blueviolet)
 [![Made With React](https://img.shields.io/badge/made%20with-react-61DAFB)](https://img.shields.io/badge/npm-6.13.7-blueviolet) 
[![Build Status](http://img.shields.io/travis/badges/badgerbadgerbadger.svg?style=flat-square)](https://travis-ci.org/badges/badgerbadgerbadger) 

---------------
### veja a demonstração [AQUI](https://prudhvignv.github.io/pathFinderVisualizer/)

##### Demonstração da visualização DFS:

   ![dfs](https://user-images.githubusercontent.com/39909903/91169511-5723df00-e68c-11ea-87ed-896412c347b2.PNG)
   


## Sobre: 
 Este é um projeto divertido sobre visualização de algoritmos de busca, por exemplo, BFS, DFS, Dikstra’s , A*.
Esta aplicação é totalmente construída em react e, abaixo, temos como é a interface..
O quadrado verde é o ponto de partida e o quadrado vermelho é o ponto de chegada.
Abaixo, você pode ver os diversos algoritmos a serem visualizados.
Aqui, o  design do mapa foi feito usando tabelas e a configuração da cor do primeiro e ultimo nós, foi feita usando propriedades CSS.
![mapa](https://user-images.githubusercontent.com/39909903/91166796-c519d780-e687-11ea-9b16-ac0504aa3a49.PNG)


## Introdução ..

Algoritmos de busca desempenham um papel vital no nosso dia a dia, como redes de computadores. O Google maps usa um algoritmo de busca para encontrar o menor caminho.
Logo, a ideia desse projeto é visualizar algoritmos usando react com a ajuda de algumas animações CSS.

Você também pode seguir o meu [BLOG no Medium](https://medium.com/@prudhvi.gnv/path-finding-visualizer-using-react-from-creating-to-building-and-deploying-bd1e2bc64696) para maiores entendimentos e detalhes :)
------

Vamos ver a intuição por trás desses algoritmos para melhores insights.
### Busca em largura (Breadth First Search)
* A busca em largura explora a igualdade em todas as direções.
* Esse é um algoritmo incrivelmente útil, não apenas para travessia regular, mas também para geração de mapa procedural, descoberta de caminhos de fluxo, mapas de distância, e outros tipos de análise de mapas.
* Este pode ser o algoritmo de escolha para identificar lugares de interesse próximos em um GPS.
* BFS garante o menor caminho.
Abaixo está o resultado para a busca em largura:
![bfs](https://user-images.githubusercontent.com/39909903/91166761-b7645200-e687-11ea-90ab-ef04daeda21e.PNG)

### Busca em profundidade (Depth First Search)
- Explora todas as possibilidades indo até o mais profundo possível em cada caminho antes de fazer o backtracking.
- Tão útil como a BFS: DFS pode ser usada para gerar ordem topológica, gerar labirintos, explorar árvores, construir árvores de decisão, encontrar um caminho-solução para escolhas hierárquicas…
- DFS não garante o menor caminho.
Below is how the DFS works
![dfs](https://user-images.githubusercontent.com/39909903/91169511-5723df00-e68c-11ea-87ed-896412c347b2.PNG)

### Dijkstra
- O algoritmo Dijkstra nos permite priorizar qual caminho será explorado. Ao invés de explorar todas as possibilidades igualmente, ele favorece os caminhos de menor custo.
- Nós podemos associar um custo menor para incentivar a passagem por certas ruas, enquanto associamos um custo maior em autoestradas para evitá-las.
- Esse é o algoritmo de escolha para encontrar o caminho mais curto em trajetos com múltiplos destinos
Abaixo está a demonstração:
![dikstra](https://user-images.githubusercontent.com/39909903/91166789-c0552380-e687-11ea-9e87-e023e381eb06.PNG)

### A* (A-Estrela)
- A* é uma modificação do algoritmo de Dijkstra otimizado para um único destino.
- O algoritmo Dijkstra encontra caminhos para todos os lugares; A* encontra caminhos para um lugar. Ele prioriza caminhos que parecem estar direcionando para mais próximo do objetivo.
- Em um jogo, poderíamos configurar custos a serem atraídos ou repelidos de objetos: muito útil para inteligência artificial.
- Esse é como o algoritmo padrão ouro em indústrias para encontrar as direções entre dois locais.
Abaixo está a demonstração da aplicação:
![a](https://user-images.githubusercontent.com/39909903/91166759-b59a8e80-e687-11ea-8ed7-faa0d453fe71.PNG)

Agora, vamos para o código ..
------------------
## Getting Started ..
Primeiro instale o node.js que vem com o bundle(npm+npx)  para rodar java localmente.
Rode os seguintes comandos no terminal para criar uma aplicação react:

```
npx create-react-app my-app
cd my-app
npm start
```

### npm start
Rode a aplicação em modo de desenvolvimento.
Abra http://localhost:3000 para ver no navegador.
A página vai recarregar se você fizer modificações
Você também verá erros de lint no console.
Abaixo o componente que é o componente raiz para aplicações react.

```js
import React from 'react';
import './App.css';
import PathfindingVisualizer from './PathfindingVisualizer/PathfindingVisualizer';
function App() {
  return (
    <div className="App">
      <PathfindingVisualizer></PathfindingVisualizer>
    </div>
  );
}
export default App;
```

O componente PathfindingVisualizer é importado e renderizado no arquivo App.js.

Eu escrevo tudo relacionado ao projeto no componente pathfindingVisualizer.
## pathfindingVisualizer:
Aqui nós reunimos tudo que precisamos para esse componente como GUI lógica, lógica de animações, estrutura e propriedades de objetos node, alguns valores boleanos (isRunning, isStartNode, isFinishNode, isWallNode ), propriedades CSS, paredes lógicas, implementação de algoritmos, mousehandlers
Os algoritmos de busca são implementados em outra pasta e importados dentro do componente pathfindingVisualizer.

```js
import React, {Component} from 'react';
import Node from './Node/Node';
import {dijkstra} from '../algorithms/dijkstra';
import {AStar} from '../algorithms/aStar';
import {dfs} from '../algorithms/dfs';
import {bfs} from '../algorithms/bfs';
import './PathfindingVisualizer.css';
```
 O componente que lida com eventos do mouse e alguns componentes reutilizáveis para deixar a aplicação mais amigável.
 
 Há funcionalidades no pathfindingVisualizer para criação: initialgrid(), clearwalls(), CreateNode(), isGridClear(), clearGrid() etc ..
 
 ***Abaixo, o código que implementa os algoritmos no componente!!***
 
 ```js
 
  visualize(algo) {
    if (!this.state.isRunning) {
      this.clearGrid();
      this.toggleIsRunning();
      const {grid} = this.state;
      const startNode =
        grid[this.state.START_NODE_ROW][this.state.START_NODE_COL];
      const finishNode =
        grid[this.state.FINISH_NODE_ROW][this.state.FINISH_NODE_COL];
      let visitedNodesInOrder;
      switch (algo) {
        case 'Dijkstra':
          visitedNodesInOrder = dijkstra(grid, startNode, finishNode);
          break;
        case 'AStar':
          visitedNodesInOrder = AStar(grid, startNode, finishNode);
          break;
        case 'BFS':
          visitedNodesInOrder = bfs(grid, startNode, finishNode);
          break;
        case 'DFS':
          visitedNodesInOrder = dfs(grid, startNode, finishNode);
          break;
        default:
          // should never get here
          break;
      }
      
 ```
Se você quiser user esse projeto de base para criar o seu próprio Visualizador de Pathfinding, fique a vontade para criar um fork desse projeto ou, simplesmente, copiar e colocar o código.
Fique a vontade para conferir meus outros projetos em [Meu Portfólio](https://prudhvignv.github.io).

Tudo abaixo dessa linha foi gerado automaticamente pelo Create React App.

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).
## Deployment
### `npm run build`
Builds the app for production to the `build` folder.<br>
It correctly bundles React in production mode and optimizes the build for the best performance.
The build is minified and the filenames include the hashes.<br>
Your app is ready to be deployed!
I deploy this app in github pages. 
You can check out here : [https://prudhvignv.github.io/pathFinderVisualizer/](https://prudhvignv.github.io/pathFinderVisualizer/)
### LICENSE
[MIT](https://github.com/PrudhviGNV/pathFinderVisualizer/blob/master/LICENSE)
-------------------------------
----------------------------
## For more documentation and understanding.. check out following links..
You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).
To learn React, check out the [React documentation](https://reactjs.org/).
### Code Splitting
This section has moved here: https://facebook.github.io/create-react-app/docs/code-splitting
### Analyzing the Bundle Size
This section has moved here: https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size
### Making a Progressive Web App
This section has moved here: https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app
### Advanced Configuration
This section has moved here: https://facebook.github.io/create-react-app/docs/advanced-configuration
### Deployment
This section has moved here: https://facebook.github.io/create-react-app/docs/deployment
### `npm run build` fails to minify
This section has moved here: https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify
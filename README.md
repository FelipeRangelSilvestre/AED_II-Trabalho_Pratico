# 🚦 Sistema de Trânsito Inteligente (AED II)

Este repositório contém o Trabalho Prático da disciplina de **Algoritmos e Estruturas de Dados II**. O projeto consiste numa simulação de tráfego urbano que integra **Grafos Ponderados** e **Árvores AVL** para calcular rotas ótimas em tempo real, considerando eventos dinâmicos como acidentes e obras.

---

## 📋 Sobre o Projeto

O objetivo principal é demonstrar a aplicação prática de estruturas de dados avançadas sem o uso de bibliotecas prontas para a lógica central (como `networkx` ou `pandas`). Todo o algoritmo de grafos e balanceamento de árvore foi implementado "do zero".

### 🚀 Funcionalidades Principais
* **Visualização Gráfica:** Interface interativa (GUI) com uma malha de 10x10 (100+ interseções).
* **Cálculo de Rotas:** Uso do algoritmo de Dijkstra para encontrar o caminho mais rápido.
* **Eventos Dinâmicos:** Registro de acidentes ou obras que alteram o "peso" (tempo) das vias.
* **Integração Automática:** Ao criar um evento, a rota é recalculada automaticamente.
* **Persistência de Dados:** Funcionalidade de Salvar e Carregar o estado do sistema (JSON).
* **Rotas Alternativas:** Cálculo das K-melhores rotas para fugir do trânsito.

---

## 🧠 Arquitetura e Estruturas de Dados (Guia de Estudo)

Esta seção explica como o código funciona internamente. Utilize isto para estudar para a defesa do projeto.

### 1. Grafo Ponderado (`GrafoPonderado`)
A malha viária é representada por um **Grafo Direcionado e Ponderado**.
* **Vértices (Nós):** Representam as esquinas/interseções (ex: `R1C1`).
* **Arestas (Linhas):** Representam as ruas que ligam as esquinas.
* **Pesos:** O "custo" de passar pela rua. Aqui, o peso é o **Tempo (minutos)**, calculado com base na distância e na velocidade da via.

> **Defesa:** "Utilizamos lista de adjacência (dicionário de dicionários) para representar o grafo, pois é mais eficiente em memória para grafos esparsos do que uma matriz de adjacência."

### 2. Árvore AVL (`ArvoreAVL`)
Para gerenciar os eventos de trânsito (acidentes, blitz, obras), utilizamos uma **Árvore Binária de Busca Balanceada (AVL)**.
* **Por que AVL?** Precisamos buscar, inserir e remover eventos rapidamente. Uma lista simples seria lenta (`O(n)`), enquanto a AVL garante performance logarítmica (`O(log n)`).
* **Chave:** Os eventos são organizados por ID.

### 3. Algoritmo de Dijkstra
Para calcular a rota:
1.  O algoritmo explora o grafo partindo da origem.
2.  Mantém uma lista de distâncias mínimas conhecidas para cada vértice.
3.  Utiliza uma **Fila de Prioridade (Heap)** para sempre expandir o caminho mais curto encontrado até o momento.
4.  Garante a rota matematicamente mais rápida.

### 4. Integração Dinâmica (O Bônus)
O diferencial do projeto é a comunicação entre o Grafo e a AVL:
1.  O usuário registra um **Evento** (ex: Acidente).
2.  O evento é inserido na **AVL**.
3.  Imediatamente, o sistema localiza a aresta correspondente no **Grafo** e aumenta o seu peso (reduz a velocidade).
4.  Se uma rota for calculada agora, o **Dijkstra** "perceberá" que aquele caminho está lento e tentará desviar.

---

## 🛠️ Instalação e Execução

### Pré-requisitos
* Python 3.x instalado.
* Biblioteca `tkinter` (geralmente já vem com o Python).

### Como Rodar
1.  Clone o repositório:
    ```bash
    git clone [https://github.com/SEU_USUARIO/NOME_DO_REPO.git](https://github.com/SEU_USUARIO/NOME_DO_REPO.git)
    ```
2.  Navegue até a pasta:
    ```bash
    cd NOME_DO_REPO
    ```
3.  Execute o arquivo principal:
    ```bash
    python gui_sistema_melhorado.py
    ```

---

## 🎮 Guia de Uso

1.  **Menu Arquivo:**
    * `Salvar Estado`: Salva a malha atual e os eventos num arquivo `.json`.
    * `Carregar Estado`: Restaura um cenário salvo anteriormente.
2.  **Aba Rotas:**
    * Selecione **Origem** e **Destino**.
    * Clique em `Calcular Rota` para ver o caminho azul (mais rápido).
    * Clique em `Mostrar Alternativas` para ver até 3 opções de caminho.
3.  **Aba Eventos:**
    * Escolha o tipo (Acidente/Obra/Engarrafamento).
    * O sistema aplicará a penalidade de velocidade na via selecionada.
    * Observe como a rota muda de cor ou traçado no mapa!

---

## 📂 Estrutura de Arquivos

* `gui_sistema_melhorado.py`: Código fonte completo (Interface + Lógica).
* `Relatorio_Tecnico.pdf`: Documentação acadêmica detalhada do projeto.
* `README.md`: Este guia.

---

## 👨‍💻 Autores

* **Felipe Rangel Silvestre**
* **Marcelo Barros**
* **Nádia Leão**
* **Marcos Oliveira**
* **Pedro**


---

*Projeto desenvolvido para a disciplina de AED II - UFAM.*

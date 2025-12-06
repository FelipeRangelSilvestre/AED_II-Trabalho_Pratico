# 🚦 Sistema de Trânsito Inteligente (AED II)

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Finalizado-success?style=for-the-badge)

Este repositório contém o Trabalho Prático da disciplina de **Algoritmos e Estruturas de Dados II**. O projeto consiste numa simulação de tráfego urbano que integra **Grafos Ponderados** e **Árvores AVL** para calcular rotas ótimas em tempo real, considerando eventos dinâmicos como acidentes e obras.

---

## 📋 Sobre o Projeto

O objetivo principal é demonstrar a aplicação prática de estruturas de dados avançadas **sem o uso de bibliotecas prontas** para a lógica central (como `networkx` ou árvores pré-prontas). Todo o algoritmo de grafos, o Dijkstra e o balanceamento da árvore AVL foram implementados "do zero".

### 🚀 Funcionalidades Principais
* **Visualização Gráfica:** Interface interativa (Tkinter) com malha de 10x10 (100+ interseções).
* **Cálculo de Rotas:** Uso do algoritmo de Dijkstra para encontrar o caminho mais rápido.
* **Eventos Dinâmicos:** Registro de acidentes ou obras que alteram o "peso" (tempo) das vias.
* **Integração Automática:** Ao criar um evento na AVL, o Grafo é atualizado e a rota recalculada.
* **Persistência de Dados:** Funcionalidade de Salvar e Carregar o estado do sistema (JSON).
* **Rotas Alternativas:** Cálculo das K-melhores rotas para sugerir desvios.

---

## 📸 Screenshots

*(Adicione aqui prints da tela do seu sistema. Ex: Rota Normal vs. Rota com Acidente)*

| Malha Viária | Rota com Desvio |
|:---:|:---:|
| <img src="caminho/para/print1.png" width="400"> | <img src="caminho/para/print2.png" width="400"> |

---

## 🧠 Arquitetura e Complexidade (Guia de Estudo)

Esta seção detalha as escolhas técnicas e a análise de complexidade para a defesa do projeto.

| Estrutura / Algoritmo | Implementação | Complexidade Média | Uso no Projeto |
| :--- | :--- | :--- | :--- |
| **Grafo Ponderado** | Lista de Adjacência | $O(V + E)$ (Espaço) | Representa esquinas (V) e ruas (E). O peso é o *tempo*. |
| **Árvore AVL** | Nó com rotação manual | $O(\log n)$ (Busca/Inserção) | Gerencia eventos ativos. Garante busca rápida por ID. |
| **Dijkstra** | Com Heap Binária | $O((V + E) \log V)$ | Encontra o caminho de menor tempo (não menor distância). |

### 1. Grafo Ponderado (`GrafoPonderado`)
Utilizamos **Lista de Adjacência** (dicionário de dicionários) em vez de Matriz de Adjacência.
> **Justificativa:** Como a malha viária é um grafo esparso (cada esquina tem poucas conexões), a lista economiza memória e torna a iteração sobre vizinhos mais eficiente.

### 2. Árvore AVL (`ArvoreAVL`)
Para gerenciar os eventos, implementamos uma AVL com rotações simples e duplas.
> **Justificativa:** Precisamos garantir que a busca e remoção de eventos seja rápida mesmo com muitos registros. A AVL mantém a altura controlada em $O(\log n)$, evitando o pior caso $O(n)$ de uma árvore binária comum.

### 3. Integração Dinâmica
A comunicação entre estruturas segue o padrão Observer:
1.  Registro de **Evento** na AVL.
2.  Busca da aresta correspondente no **Grafo**.
3.  Atualização do **peso da aresta** (ex: velocidade cai de 60km/h para 10km/h).
4.  O **Dijkstra** lê o novo peso automaticamente na próxima consulta.

---

## 🛠️ Instalação e Execução

### Pré-requisitos
* Python 3.10 ou superior.
* Biblioteca `tkinter` (Nativa no Windows/Mac. No Linux: `sudo apt-get install python3-tk`).

### Como Rodar
1.  Clone o repositório:
    ```bash
    git clone [https://github.com/FelipeRangelSilvestre/AED_II-Trabalho_Pratico.git](https://github.com/FelipeRangelSilvestre/AED_II-Trabalho_Pratico.git)
    ```
2.  Navegue até a pasta:
    ```bash
    cd AED_II-Trabalho_Pratico
    ```
3.  Execute o arquivo principal:
    ```bash
    python sistema_transito_inteligente.py
    ```

---

## 🎮 Guia de Uso

1.  **Menu Arquivo:**
    * `Salvar Estado`: Salva a topologia e eventos em `.json`.
    * `Carregar Estado`: Restaura um cenário complexo salvo anteriormente.
2.  **Aba Rotas:**
    * Selecione **Origem** e **Destino**.
    * Clique em `Calcular Rota` para ver o trajeto ótimo (Azul).
    * Clique em `Mostrar Alternativas` para ver opções secundárias (Verde/Laranja).
3.  **Aba Eventos:**
    * Escolha o tipo (Acidente/Obra/Engarrafamento).
    * O sistema aplicará a penalidade na via e atualizará o grafo em tempo real.

---

## 📂 Estrutura de Arquivos

* `sistema_transito_inteligente.py`: Código fonte completo (Interface + Lógica AVL/Grafo).
* `Relatorio_Tecnico.pdf`: Documentação acadêmica detalhada.
* `README.md`: Documentação do repositório.
* `cenario_exemplo.json`: Arquivo de exemplo para teste de carga (opcional).

---

## 👨‍💻 Autores

* **Felipe Rangel Silvestre**
* **Marcelo Barros**
* **Nádia Leão**
* **Marcos Oliveira**
* **Pedro Jheveson**

---

*Projeto desenvolvido para a disciplina de AED II - UFAM (ICET).*

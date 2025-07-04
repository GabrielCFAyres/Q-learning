# Projeto Q-Learning — Sistemas Inteligentes
## Descrição
Este projeto consiste na implementação de um agente de Q-learning para resolver um jogo de plataformas, onde o objetivo é ensinar o personagem Amongois a navegar entre plataformas e chegar ao bloco final (preto). O agente toma decisões entre girar à esquerda, girar à direita ou pular para frente, aprendendo progressivamente o melhor caminho por meio de tentativa e erro, baseado em recompensas.

O código foi desenvolvido em Python, utilizando comunicação via socket com o ambiente do jogo (executável fornecido pela disciplina). O aprendizado é armazenado em uma Q-table que pode ser salva e reutilizada.

## Estrutura do Projeto

`connection.py`: Funções auxiliares para conectar ao ambiente do jogo e obter estados/recompensas.
`client.py`: Implementação principal do algoritmo Q-learning e lógica de treinamento.
`q_table.txt:` Arquivo onde a Q-table é salva para persistência do aprendizado.

## Como Funciona
### 1. Inicialização
- Define hiperparâmetros do Q-learning: taxa de aprendizado (`alpha`), fator de desconto (`gamma`), taxa de exploração (`epsilon`), etc.
- Carrega a Q-table já existente (caso haja) ou inicia uma tabela zerada (96 estados x 3 ações).
- Estados são representados por combinações de plataforma e direção (total de 96 possíveis).

### 2. Escolha de Ação
- Usa uma política **epsilon-greedy** com customizações:
   * Com probabilidade `epsilon`, o agente explora ações aleatórias (mas ponderando para priorizar ‘jump’).
   * Fora isso, seleciona a ação de maior valor na Q-table para o estado atual.
   * Regras adicionais evitam que o agente fique preso repetindo a mesma ação.

### 3. Atualização da Q-table
- Após cada ação, atualiza a Q-table conforme a equação do Q-learning, penalizando repetições de estado e recompensando avanços.
- A Q-table é persistida no disco ao final do treino.

### 4. Treinamento
- O agente faz centenas de tentativas, em cada uma buscando atingir o objetivo a partir da plataforma inicial.
- Ao longo do tempo, `epsilon` diminui, levando o agente a explorar menos e confiar mais no que já aprendeu.

## Time Envolvido
- Gabriel Ayres
- Danilo Coutinho
- Gustavo Araújo

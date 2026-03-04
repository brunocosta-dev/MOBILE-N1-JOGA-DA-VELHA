<pre>
  DART
</pre>

```Dart
import 'dart:io';

void main() {
  List<List<String>> board = List.generate(
    3,
    (_) => List.generate(3, (_) => ' '),
  );

  String currentPlayer = 'X';
  bool gameOver = false;
  bool gameFinished = false;

  while (!gameOver) {
      
    // TODO 1:
    // Verificar se a posição escolhida é válida e está vazia.
    // Se não for válida, mostrar mensagem e continuar o loop.

    // TODO 2:
    // Registrar a jogada no tabuleiro.
    do{
        clearScreen();
        drawBoard(board);
    
        print('Jogador $currentPlayer, escolha linha e coluna (0, 1 ou 2):');
       
        int row = int.parse(stdin.readLineSync()!);
        int col = int.parse(stdin.readLineSync()!);
        
        if(board[row][col] == ' '){
            board[row][col] = currentPlayer;
            gameFinished = true;
        }else{
            print("Posicao já ocupada! Escolha outra");
        }
        
    }while(!gameFinished);
    
    gameFinished = false;
    
    // TODO 3:
    // Verificar se o jogador atual venceu.
    // Se venceu, exibir mensagem e encerrar o jogo.
    // TODO 4:
    // Verificar se houve empate.
    // Se empate, exibir mensagem e encerrar o jogo.
    // TODO 5:
    // Alternar o jogador (X <-> O)
    
    if(checkWinner(board, currentPlayer)){
        gameOver = true;
        print('Parabéns! O jogador $currentPlayer venceu!');
    }else if(checkDraw(board)){
        gameOver = true;
        print('Deu velha! Os jogador X e O empataram!');
    }else{
       gameOver = false;
       currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }


  }

  clearScreen();
  drawBoard(board);
  print('Fim de jogo!');
}

void drawBoard(List<List<String>> board) {
  print('  0   1   2');
  for (int i = 0; i < 3; i++) {
    print('${i} ${board[i][0]} | ${board[i][1]} | ${board[i][2]}');
    if (i < 2) print(' ---+---+---');
  }
}

void clearScreen() {
  // Simula limpeza do console
  print('\x1B[2J\x1B[0;0H');
}

bool checkWinner(List<List<String>> board, String player) {
  // TODO 6:
  // Implementar verificação de vitória:
  // - 3 linhas
  // - 3 colunas
  // - 2 diagonais
  
  final combination = [
      [0,1,2],[3,4,5],[6,7,8],  // linhas
      [0,3,6],[1,4,7],[2,5,8], // colunas
      [0,4,8],[2,4,6]         // Diagonais
    ];
    
    for (var comb in combination){
        bool isWinner = true;
        
        for (var index in comb){
            int row = index ~/ 3;
            int coll = index % 3;
            
            if(board[row][coll] != player){
                isWinner = false;
                break;
            }
        }
        if(isWinner) return true;
        
    }

  return false;
}

bool checkDraw(List<List<String>> board) {
  // TODO 7:
  // Retornar true se todas as posições estiverem preenchidas.
  return board.every((row)=> row.every((campo) => campo != ' '));
}
```

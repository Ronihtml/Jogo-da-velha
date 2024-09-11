import java.util.Scanner;

public class TicTacToe {

    private static char[][] board = {{' ', ' ', ' '}, {' ', ' ', ' '}, {' ', ' ', ' '}};
    private static char currentPlayer = 'X';

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean gameEnded = false;

        while (!gameEnded) {
            printBoard();
            playerMove(scanner);
            gameEnded = checkForWin() || checkForDraw();
            if (!gameEnded) {
                switchPlayer();
            }
        }

        printBoard();
        if (checkForWin()) {
            System.out.println("Jogador " + currentPlayer + " venceu!");
        } else {
            System.out.println("Empate!");
        }

        scanner.close();
    }

    private static void printBoard() {
        System.out.println("  0 1 2");
        for (int i = 0; i < 3; i++) {
            System.out.print(i + " ");
            for (int j = 0; j < 3; j++) {
                System.out.print(board[i][j]);
                if (j < 2) System.out.print("|");
            }
            System.out.println();
            if (i < 2) System.out.println("  -----");
        }
    }

    private static void playerMove(Scanner scanner) {
        int row, col;
        while (true) {
            System.out.println("Jogador " + currentPlayer + ", escolha sua jogada (linha e coluna): ");
            row = scanner.nextInt();
            col = scanner.nextInt();
            if (row >= 0 && row < 3 && col >= 0 && col < 3 && board[row][col] == ' ') {
                board[row][col] = currentPlayer;
                break;
            } else {
                System.out.println("Jogada inválida. Tente novamente.");
            }
        }
    }

    private static void switchPlayer() {
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    private static boolean checkForWin() {
        // Checa linhas e colunas
        for (int i = 0; i < 3; i++) {
            if (checkRow(i) || checkColumn(i)) {
                return true;
            }
        }
        // Checa diagonais
        return checkDiagonal();
    }

    private static boolean checkRow(int row) {
        return board[row][0] == currentPlayer &&
               board[row][1] == currentPlayer &&
               board[row][2] == currentPlayer;
    }

    private static boolean checkColumn(int col) {
        return board[0][col] == currentPlayer &&
               board[1][col] == currentPlayer &&
               board[2][col] == currentPlayer;
    }

    private static boolean checkDiagonal() {
        return (board[0][0] == currentPlayer &&
                board[1][1] == currentPlayer &&
                board[2][2] == currentPlayer) ||
               (board[0][2] == currentPlayer &&
                board[1][1] == currentPlayer &&
                board[2][0] == currentPlayer);
    }

    private static boolean checkForDraw() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (board[i][j] == ' ') {
                    return false;
                }
            }
        }
        return true;
    }
}

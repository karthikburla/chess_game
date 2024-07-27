# chess_game
This is a project related to chess game

School:                                    Computing
Academic year:                   2023-2024
Submitted To :                    K.Haritha
Name of the students :	B.Bhavani karthik	Register No :	23102A040575

Course code & Title:	Object oriented programing Java-22AI1040002	Section :
	Section-1
program	B.Tech.,	Branch	Computer science Engineering
Semester :	IInd semester		
															
 
ABSTRACT
A chess game in Java is a computer program that simulates the board game chess, allowing two players to play against each other. The game can be implemented using object-oriented programming concepts, with classes representing the chessboard, pieces, and players.
The chessboard can be represented as a 2D array of squares, with each square containing a piece or being empty. The pieces can be represented as objects of classes that extend a base Piece class, with each class implementing the rules for moving that type of piece.
The game can be played through a graphical user interface (GUI) that allows players to click on pieces and squares to make moves. The GUI can be implemented using a library such as Java Swing or JavaFX.

To ensure that moves are legal according to the rules of chess, the game can include methods for checking whether a move would result in the player's king being in check, and whether the king can make any move to escape this situation. The game can also include methods for checking whether a player is in checkmate, and for handling game conclusion scenarios like checkmate or stalemate.



SYSTEM REQUIREMENTS
The hardware and software specification specifies the minimum hardware and software required to run the project. The hardware configuration specified below is not by any means the optimal hardware requirements. The software specification given below is just the minimum requirements, and the performance of the system may be slow on such system.
Hardware Requirements
•	System	                :   Pentium IV 2.4 GHz 
•	Hard Disk 	    :   40 GB
•	Floppy Drive      :   1.44 MB
•	Monitor	     :   15 VGA color
•	Mouse	                :   Logitech.
•	Keyboard	    :   110 keys enhanced
•	RAM		    :   256 MB
Software Requirements
•	Operating System  	: Windows
•	Language		: Java
•	JDK version		:8+
•	IDE			:Eclipse or visual studio code



SAMPLE CODE :
import java.awt.*;
import javax.swing.*;

public abstract class ChessPiece extends JLabel {
    private Color color;
    private int row;
    private int col;

    public ChessPiece(Color color, int row, int col) {
        this.color = color;
        this.row = row;
        this.col = col;
        setOpaque(true);
        setPreferredSize(new Dimension(50, 50));
        setHorizontalAlignment(JLabel.CENTER);
        setVerticalAlignment(JLabel.CENTER);
    }

    public abstract boolean isValidMove(int newRow, int newCol);
    public Color getColor() {
        return color;
    }
    public int getRow() {
        return row;
    }
    public int getCol() {
        return col;
    }
    public void setRow(int row) {
        this.row = row;
    }
    public void setCol(int col) {
        this.col = col;
    }
}
 
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class ChessBoard extends JPanel {
    private ChessPiece[][] board;
    private ChessPiece selectedPiece;

    public ChessBoard() {
        board = new ChessPiece[8][8];
        setLayout(new GridLayout(8, 8));
        setBackground(Color.WHITE);

        for (int i = 0; i < 8; i++) {
            for (int j = 0; j < 8; j++) {
                if ((i + j) % 2 == 0) {
                    board[i][j] = new EmptyPiece(Color.LIGHT_GRAY, i, j);
                } else {
                    board[i][j] = new EmptyPiece(Color.GRAY, i, j);
                }
                add(board[i][j]);
            }
        }

        addMouseListener(new MouseAdapter() {
            @Override
            public void mouseClicked(MouseEvent e) {
                int row = e.getY() / 50;
                int col = e.getX() / 50;
                ChessPiece piece = board[row][col];
                if (piece instanceof EmptyPiece) {
                    if (selectedPiece != null) {
                        selectedPiece.setRow(row);
                        selectedPiece.setCol(col);
                        selectedPiece.repaint();
                        selectedPiece = null;
                    }
                } else {
                    if (selectedPiece == null) {
                        selectedPiece = piece;
                    } else {
                        if (selectedPiece.getColor() != piece.getColor() && selectedPiece.isValidMove(row, col)) {
                            board[selectedPiece.getRow()][selectedPiece.getCol()] = new EmptyPiece(Color.LIGHT_GRAY, selectedPiece.getRow(), selectedPiece.getCol());
                            board[row][col] = selectedPiece;
                            selectedPiece.setRow(row);
                            selectedPiece.setCol(col);
                            selectedPiece.repaint();
                            selectedPiece = null;
                        } else {
                            selectedPiece.setRow(selectedPiece.getRow());
                            selectedPiece.setCol(selectedPiece.getCol());
                            selectedPiece.repaint();
                            selectedPiece = null;
                        }
                    }
                }
            }
        });
    }

    public void addPiece(ChessPiece piece) {
        board[piece.getRow()][piece.getCol()] = piece;
        add(piece);
    }
}
import javax.swing.*;

public class Main {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Chess Game");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 400);
        frame.setLocationRelativeTo(null);

        ChessBoard board = new ChessBoard();

        // Add your code here to add pieces to the board

        frame.add(board);
        frame.setVisible(true);
    }
}
import java.awt.*;

public class Pawn extends ChessPiece {
    public Pawn(Color color, int row, int col) {
        super(color, row, col);
        if (color == Color.WHITE) {
            setIcon(new ImageIcon("white_pawn.png"));
        } else {
            setIcon(new ImageIcon("black_pawn.png"));
        }
    }

    @Override
    public boolean isValidMove(int newRow, int newCol) {
        if (getColor() == Color.WHITE) {
            if (newRow == getRow() + 1 && newCol == getCol()) {
                return true;
            } else if (getRow() == 1 && newRow == getRow() + 2 && newCol == getCol()) {
                return true;
            }
        } else {
            if (newRow == getRow() - 1 && newCol == getCol()) {
                return true;
            } else if (getRow() == 6 && newRow == getRow()



➔Online  chess  game  is  designed  by  keeping  in  mind  the  Human  Machine  Interaction  principles.
 ➔The  web  application  is  simple  and  allows  the  user  to  play  chess.  The  user  has  the  choice  to change the theme of the game as  well.  While playing,  the user  gets to  know about  the possible movement of the pieces. 
➔Two  modes  are  available:  single  player  and  multiplayer.  In  case  of  multiplayer,  the  user  can communicate  with  the  opponent  through  a  chat  window.  For  multiple  player  mode,  if  the opponent  leaves  the  game  in the  middle,  the  browser  notiﬁes  that  the  opponent  has  left  the game.


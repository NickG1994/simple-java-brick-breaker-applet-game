# simple-java-brick-breaker-applet-game
having problems with brick collision detection any help is appreciated along with any help.
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package brickbreaker;

import java.awt.Color;
import java.awt.Dimension;
import java.awt.Graphics;
import java.awt.Image;
import java.awt.Rectangle;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseEvent;
import java.awt.event.MouseMotionListener;
import javax.swing.JApplet;
import javax.swing.Timer;

/**
 *
 * @author Dominic
 */
public class BrickBreaker extends JApplet implements MouseMotionListener {
// The object we will use to write with instead of the standard screen graphics 
     Graphics bufferGraphics; 
     // The image that will contain everything that has been drawn on 
     // bufferGraphics. 
     Image offscreen; 
     
     // To get the width and height of the applet. 
     Dimension dim; 
     
 private int x = 109; // Ball's X coordinate
 private final int WIDTH = 40; // Ball's width
      private final int HEIGHT = 40; // Ball's height
 private final int TIME_DELAY = 12; // Time delay (milliseconds)
 private final int MOVE = 5; // Pixels to move the ball

 private int y = 400; // Ball's Y coordinate
 private Timer timer; // Timer object
 private boolean goingUp = true; // Direction indicator
private boolean goingLeft = true;
 int curX;
 //private int brick[][];
   
 public int brick[][];
private final int WW = 800;
private final int WH = 600;
 private final int MINIMUM_Y = 0; // Minimum height of ball
 private final int MAXIMUM_Y = WW-HEIGHT; // Maximum height of ball
  private final int MINIMUM_X = 0; // Minimum height of ball
 private final int MAXIMUM_X = WH-WIDTH; // Maximum height of ball
 
 
 public void init()
 {
     
     super.setSize(WW,WH);
     // We'll ask the width and height by this 
     dim = getSize();
     addMouseMotionListener(this); 
//     brick = new int[5][5];
//     for (int x = 0; x < 5; x++) {
//         for (int y = 0; y < 5; y++) {
//            brick[x][y] = 1;   
//         }
//     }
     
    // brick[3][2] = 0;
         // Create an offscreen image to draw on 
          // Make it the size of the applet, this is just perfect larger 
          // size could slow it down unnecessary. 
          offscreen = createImage(dim.width,dim.height);
            // by doing this everything that is drawn by bufferGraphics 
          // will be written on the offscreen image. 
          bufferGraphics = offscreen.getGraphics(); 
 // Create a Timer object and register an ActionListener.
 timer = new Timer(TIME_DELAY, new TimerListener());

 // Start the timer.
 timer.start();
 }

 /**
 * paint method
     
 */

 public void paint(Graphics g)
 {
     // We'll ask the width and height by this 
     dim = getSize();
     
     bufferGraphics.clearRect(0, 0, dim.width, dim.height);
//     for (int x = 0; x < 5; x++) {
//        
//         
//         for (int y = 0; y < 5; y++) {
//              if (brick[x][y] == 2) {
//             bufferGraphics.setColor(Color.yellow);
//              bufferGraphics.fillRect(0+(WW/5)* y, 0+(WH/3/5)*x,WW/5-1,WH/3/5-2);
//         }
//             if (brick[x][y] == 1) {
//                 bufferGraphics.setColor(Color.blue);
//                 bufferGraphics.fillRect(0+(WW/5)* y, 0+(WH/3/5)*x,WW/5-1,WH/3/5-2);
//             }
//         }
//         
//     }
      bufferGraphics.setColor(Color.yellow);
      bufferGraphics.fillRect(0+(WW/5)* y, 0+(WH/3/5)*x,WW/5-1,WH/3/5-2);
      bufferGraphics.setColor(Color.red); 
      bufferGraphics.fillRect(curX-50, WH-80, 100, 10);
      bufferGraphics.fillOval(x, y, WIDTH, HEIGHT);
      g.drawImage(offscreen, 0, 0, this);
 }
 public void update(Graphics g){
 paint(g);
 }

    @Override
    public void mouseDragged(MouseEvent me) {
        throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }
 
 /**
 * The "following" private inner class handles the Timer object's
 * action events.
 */

 private class TimerListener implements ActionListener
 {
 @Override
 public void actionPerformed(ActionEvent e)
 {
     Rectangle ball = new Rectangle(x,y,WIDTH,HEIGHT);
     Rectangle paddle = new Rectangle(curX-50, WH-80, 100, 10);
     Rectangle brick = new Rectangle(0+(WW/5)* y, 0+(WH/3/5)*x,WW/5-1,WH/3/5-2);
             
     
     if (ball.intersects(paddle)) {
         goingUp = true;
     }
     
//     for (int x = 0; x < 5; x++) {
//         for (int y = 0; y < 5; y++) {
//             if (ball.intersects(brick[x][y])){
//                brick[x][y] = 0;
//            }
//         }
//     }
     
 // Update the ball's Y coordinate.
 if (goingUp)
 {
 if (y > MINIMUM_Y)
 y -= MOVE;
 else
 goingUp = false;
 }
 else
 {
 if (y < MAXIMUM_Y)//this is the buttom portion of the game to determine lost 
 y += MOVE;
 else
 goingUp = true;
 }
 if (goingLeft)
 {
 if (x > MINIMUM_Y)
 x -= MOVE;
 else
 goingLeft = false;
 }
 else
 {
 if (x < MAXIMUM_Y)
 x += MOVE;
 else
 goingLeft = true;
 }

 // Force a call to the paint method.
 repaint();
 }
 }
 public void mouseMoved(MouseEvent evt)  
     { 
          curX = evt.getX();  
          repaint(); 
     } 
   
    
}

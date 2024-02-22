# include "iGraphics.h"
# include "stdlib.h"
#include "string.h"
int x = 300, y = 300, r = 20,m,c,index=0,x_axis=600,y_axis=400,x_diff=20,y_diff=20,mx_i,my_i,mx_now,my_now,x_axis_move,y_axis_move;
int index_2=0;
bool type=false;

//for straight lines

/*
	function iDraw() is called again and again by the system.

	*/

void iDraw() {
	//place your drawing codes here
	int i=1;
	iClear();
	iSetColor(255,255,255);
	iFilledRectangle(0,0,1200,800);
	while(i--){
		iSetColor(0,0,0);
		iFilledRectangle(x_axis,-5000,6,10000);
		iFilledRectangle(-5000,y_axis,10000,6);
		int j=1;
		int x_lines,y_lines;
		// iLine(x_axis+x_diff+6,-5000,x_axis+x_diff+6,10000);
		// iLine(x_axis+x_diff*2+6,-5000,x_axis+x_diff*2+6,10000);
		for(j;j<=600;j++){
		 	//iLine(x_axis+x_diff*i,-4000,x_axis+x_diff*i,4000);
			//iFilledRectangle(x_axis+x_diff*j+6,-5000,3,10000);
			if(j%5){
				if(x_diff>=45){
				iSetColor(0,0,0);
				iLine(x_axis+x_diff*j+6,-5000,x_axis+x_diff*j+6,5000);
				iLine(x_axis-x_diff*j,-5000,x_axis-x_diff*j,5000);
				iLine(-5000,y_axis+y_diff*j+6,5000,y_axis+y_diff*j+6);
				iLine(-5000,y_axis-y_diff*j,5000,y_axis-y_diff*j);
				}
			}
			else {
				iSetColor(60,0,120);
				iFilledRectangle(x_axis+x_diff*j+6,-5000,3,10000);
				iFilledRectangle(x_axis-x_diff*j,-5000,3,10000);
				iFilledRectangle(-5000,y_axis-y_diff*j,10000,3);
				iFilledRectangle(-5000,y_axis+y_diff*j+6,10000,3);
			}
			
			
		}
	}
	//iSetColor(0,0,0);
	
	iSetColor(144,238,144);
	iFilledRectangle(1200,0,300,800);
	

}





/*
	function iMouseMove() is called when the user presses and drags the mouse.
	(mx, my) is the position where the mouse pointer is.
	*/
void iMouseMove(int mx1, int my1) {
	//printf("x = %d, y= %d\n",mx1,my1);
	//place your codes here
	//circle_x=mx;
	//circle_y=my;
	mx_now=mx1;
	my_now=my1;
	x_axis_move=mx_now-mx_i;
	y_axis_move=my_now-my_i;
	printf("x now %d y now %d\n x diff %d y diff %d",mx_now,my_now,x_axis_move,y_axis_move);
	x_axis+=x_axis_move;
	y_axis+=y_axis_move;
	mx_i=mx_now;
	my_i=my_now;
	
}

/*
	function iMouse() is called when the user presses/releases the mouse.
	(mx, my) is the position where the mouse pointer is.
	*/
void iMouse(int button, int state, int mx2, int my2) {
	if (button == GLUT_LEFT_BUTTON && state == GLUT_DOWN) {
		//place your codes here
		//printf("initial x = %d,initial y= %d\n",mx_i,my_i);
		mx_i=mx2;
		my_i=my2;
		printf(" x initial %d y initial %d",mx_i,my_i);
	}
	if(button==GLUT_LEFT_BUTTON && state== GLUT_DOWN){
		if(mx2>1200 && mx2<=1500){
			type=true;
		}
	}

}

/*
	function iKeyboard() is called whenever the user hits a key in keyboard.
	key- holds the ASCII value of the key pressed.
	*/
void iKeyboard(unsigned char key) {
	if (key == 'q') {
		exit(0);
	}
	
	if(key=='z'){
		x_diff+=5;
		y_diff+=5;
	}
	if(key=='x'){
		x_diff-=5;
		y_diff-=5;
	}
	
	
	
	


}

/*
	function iSpecialKeyboard() is called whenver user hits special keys like-
	function keys, home, end, pg up, pg down, arraows etc. you have to use
	appropriate constants to detect them. A list is:
	GLUT_KEY_F1, GLUT_KEY_F2, GLUT_KEY_F3, GLUT_KEY_F4, GLUT_KEY_F5, GLUT_KEY_F6,
	GLUT_KEY_F7, GLUT_KEY_F8, GLUT_KEY_F9, GLUT_KEY_F10, GLUT_KEY_F11, GLUT_KEY_F12,
	GLUT_KEY_LEFT, GLUT_KEY_UP, GLUT_KEY_RIGHT, GLUT_KEY_DOWN, GLUT_KEY_PAGE UP,
	GLUT_KEY_PAGE DOWN, GLUT_KEY_HOME, GLUT_KEY_END, GLUT_KEY_INSERT
	*/
void iSpecialKeyboard(unsigned char key) {

	if (key == GLUT_KEY_END) {
		exit(0);
	}

}


int main() {
	//place your own initialization codes here.

      //scanf("%d%d",m,c);
	
	iInitialize(1500, 800, "project_trial_1");
	return 0;
}

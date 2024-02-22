# include "iGraphics.h"
# include "stdlib.h"
#include "string.h"
#include "math.h"
int x = 300, y = 300, r = 0,m,c,index=0,x_axis=600,y_axis=400,x_diff=20,y_diff=20,mx_i,my_i,mx_now,my_now,x_axis_move,y_axis_move;
int index_2=0,window=0;
bool type=false,draw[10]={false,false,false,false,false,false,false,false,false,false};
// bool variable_8=false,variable_9=false,variable_10=false,variable_11=false,variable_12=false,variable_13=false,variable_14=false;
// bool variable_1=false,variable_2=false,variable_3=false,variable_4=false,variable_5=false,variable_6=false,variable_7=falsevariable_15=false,variable_16=false,variable_17=false,variable_18=false,variable_19=false,variable_20=false,variable_21=false,variable_22=false;
bool variable[10][50];
bool go_back=false;
int function[10]={0,0,0,0,0,0,0,0,0,0},format[10]={0,0,0,0,0,0,0,0,0,0},function2=0;
// char v1[10],v2[10],v3[10],v4[10],v5[10],v6[10],v7[10],v8[10],v9[10],v10[10],v11[10],v12[10],v13[10],v14[10],v15[10],v16[10],v17[10],v18[10],v19[10],v20[10],v21[10],v22[10];
char v[10][50][10];
//float var1,var2,var3,var4,var5,var6,var7,var8,var9,var10,var11,var12,var13,var14,var15,var16,var17,var18,var19,var20,var21,var22;
//int i1,i2;
float var[10][50];

// for(int i1=0;i1<10;i1++)
// {
// 	for(int i2=0;i2<50;i2++)
// 	{
// 		var[i1][i2]=0;
// 	}
// }
void clear_variables()
{
	for(int i1=0;i1<10;i1++)
	{
	for(int i2=0;i2<50;i2++)
		{
			v[i1][i2][0]='\0';
		}
	}
}






int origin_x=x_axis,origin_y=y_axis;
const double PI=M_PI,e=exp(1.0);







/*
	function iDraw() is called again and again by the system.

	*/
void draw_menu()
{
    iSetColor(164,260,164);
    iFilledRectangle(1210,730,280,60);
    iFilledRectangle(1210,660,280,60);
    iFilledRectangle(1210,590,280,60);
    iFilledRectangle(1210,520,280,60);
    iFilledRectangle(1210,450,280,60);
    iFilledRectangle(1210,380,280,60);
    iSetColor(0,0,0);
    iText(1220,740,"Select your Function:",GLUT_BITMAP_TIMES_ROMAN_24);
    iText(1220,670,"Linear:",GLUT_BITMAP_HELVETICA_18);
    iText(1220,600,"Polynomial:",GLUT_BITMAP_HELVETICA_18);
    iText(1220,530,"Trigonometric:",GLUT_BITMAP_HELVETICA_18);
    iText(1220,460,"Exponential:",GLUT_BITMAP_HELVETICA_18);
    iText(1220,390,"Logarithmic:",GLUT_BITMAP_HELVETICA_18);
}

void draw_linear_menu()
{
    iSetColor(164,260,164);
    iFilledRectangle(1210,730,280,60);
    iFilledRectangle(1210,660,280,60);
    iFilledRectangle(1210,590,280,60);
    iFilledRectangle(1210,520,280,60);
    iFilledRectangle(1210,450,280,60);
	iFilledRectangle(1210,30,50,30);
    iSetColor(0,0,0);
    iText(1220,740,"Select your Format:",GLUT_BITMAP_TIMES_ROMAN_24);
    iText(1220,670,"1.y=mx+c",GLUT_BITMAP_HELVETICA_18);
    iText(1220,600,"2.ax+by+c=0",GLUT_BITMAP_HELVETICA_18);
    iText(1220,530,"3.x/a + y/b =1",GLUT_BITMAP_HELVETICA_18);
    iText(1220,460,"4.x=a",GLUT_BITMAP_HELVETICA_18);
	iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);

}

void draw_polynomial_menu()
{
    iSetColor(164,260,164);
    iFilledRectangle(1210,730,280,60);
    iFilledRectangle(1210,660,280,60);
    iFilledRectangle(1210,590,280,60);
	iFilledRectangle(1210,30,50,30);
    iSetColor(0,0,0);
    iText(1220,740,"Select your Format:",GLUT_BITMAP_TIMES_ROMAN_24);
    iText(1220,670,"1.y=ax^2 + bx + c",GLUT_BITMAP_HELVETICA_18);
    iText(1220,600,"2.x=ay^2 + by + c",GLUT_BITMAP_HELVETICA_18);
	iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);

}
void draw_trig_menu()
{
    iSetColor(164,260,164);
    iFilledRectangle(1210,730,280,60);
    iFilledRectangle(1210,660,280,60);
    iFilledRectangle(1210,590,280,60);
    iFilledRectangle(1210,520,280,60);
    iFilledRectangle(1210,450,280,60);
    iFilledRectangle(1210,380,280,60);
    iFilledRectangle(1210,310,280,60);
	iFilledRectangle(1210,30,50,30);
    iSetColor(0,0,0);
    iText(1220,740,"Select your Format:",GLUT_BITMAP_TIMES_ROMAN_24);
    iText(1220,670,"1.y=msin(ax+b)+c",GLUT_BITMAP_HELVETICA_18);
    iText(1220,600,"2.y=mcos(ax+b)+c",GLUT_BITMAP_HELVETICA_18);
    iText(1220,530,"3.y=mtan(ax+b)+c",GLUT_BITMAP_HELVETICA_18);
    iText(1220,460,"4.y=mcot(ax+b)+c",GLUT_BITMAP_HELVETICA_18);
    iText(1220,390,"5.y=mcosec(ax+b)+c",GLUT_BITMAP_HELVETICA_18);
    iText(1220,320,"5.y=msec(ax+b)+c",GLUT_BITMAP_HELVETICA_18);
	iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
}
void draw_exp_menu()
{
    iSetColor(164,260,164);
    iFilledRectangle(1210,730,280,60);
    iFilledRectangle(1210,660,280,60);
    iFilledRectangle(1210,590,280,60);
	iFilledRectangle(1210,30,50,30);
    iSetColor(0,0,0);
    iText(1220,740,"Select your Format:",GLUT_BITMAP_TIMES_ROMAN_24);
    iText(1220,670,"1.y=a^(bx)",GLUT_BITMAP_HELVETICA_18);
    iText(1220,600,"2.y=e^(bx)",GLUT_BITMAP_HELVETICA_18);
	iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
}
void draw_log_menu()
{
    iSetColor(164,260,164);
    iFilledRectangle(1210,730,280,60);
    iFilledRectangle(1210,660,280,60);
    iFilledRectangle(1210,590,280,60);
    iFilledRectangle(1210,450,280,120);
	iFilledRectangle(1210,30,50,30);
    iSetColor(0,0,0);
    iText(1220,740,"Select your Format:",GLUT_BITMAP_TIMES_ROMAN_24);
    iText(1220,670,"1.y=log(ax)",GLUT_BITMAP_HELVETICA_18);
    iText(1220,600,"2.y=ln(ax)",GLUT_BITMAP_HELVETICA_18);
    iText(1220,530,"3.Select base manually:",GLUT_BITMAP_HELVETICA_18);
	iText(1220,460,"y=log_a(bx)",GLUT_BITMAP_HELVETICA_18);
	iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);



}

void take_inputs()
{
    if(format[r]==1)
    {
        iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
        iSetColor(0,0,0);
        iText(1220,740,"Input the values of m and c:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,670,"m:",GLUT_BITMAP_HELVETICA_18);
        iSetColor(164,260,164);
        iFilledRectangle(1210,590,280,60);
		iSetColor(0,0,0);
		iText(1220,600,v[r][1],GLUT_BITMAP_8_BY_13);
        iSetColor(0,0,0);
        iText(1220,530,"c:",GLUT_BITMAP_HELVETICA_18);
        iSetColor(164,260,164);
        iFilledRectangle(1210,450,280,60);
		iSetColor(0,0,0);
		iText(1220,460,v[r][2],GLUT_BITMAP_8_BY_13);
		iSetColor(164,280,164);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		//if(draw1)
		
			
		
		
    }
	if(format[r]==2)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1210,450,280,60);
		iFilledRectangle(1210,310,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
        iSetColor(0,0,0);
        iText(1220,740,"Input the values of a,b,c:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,670,"a:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,530,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,390,"c:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,600,v[r][3],GLUT_BITMAP_8_BY_13);
        iText(1220,460,v[r][4],GLUT_BITMAP_8_BY_13);
		iText(1220,320,v[r][5],GLUT_BITMAP_8_BY_13);
        
        
		
	}
	if(format[r]==3)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1210,450,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
        iText(1220,740,"Input the values of a,b:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,670,"a:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,530,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][6],GLUT_BITMAP_8_BY_13);
        iText(1220,460,v[r][7],GLUT_BITMAP_8_BY_13);

		
	}
	if(format[r]==4)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1220,740,"Input the values of a:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,670,"a:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][8],GLUT_BITMAP_8_BY_13);

		
	}
    if(format[r]==5)
    {
        iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1210,450,280,60);
		iFilledRectangle(1210,310,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
        iSetColor(0,0,0);
        iText(1220,740,"Input the values of a,b,c:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,670,"a:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,530,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,390,"c:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,600,v[r][9],GLUT_BITMAP_8_BY_13);
        iText(1220,460,v[r][10],GLUT_BITMAP_8_BY_13);
		iText(1220,320,v[r][11],GLUT_BITMAP_8_BY_13);

       
    }
	if(format[r]==6)
    {
        iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1210,450,280,60);
		iFilledRectangle(1210,310,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
        iSetColor(0,0,0);
        iText(1220,740,"Input the values of a,b,c:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,670,"a:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,530,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,390,"c:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,600,v[r][12],GLUT_BITMAP_8_BY_13);
        iText(1220,460,v[r][13],GLUT_BITMAP_8_BY_13);
		iText(1220,320,v[r][14],GLUT_BITMAP_8_BY_13);

        
    }
	if(format[r]==7)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1210,450,280,60);
		iFilledRectangle(1210,310,280,60);
		iFilledRectangle(1210,190,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1220,740,"Input the values of m,a,b,c:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,680,"m:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,540,"a:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,400,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,270,"c:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][15],GLUT_BITMAP_8_BY_13);
        iText(1220,460,v[r][16],GLUT_BITMAP_8_BY_13);
		iText(1220,320,v[r][17],GLUT_BITMAP_8_BY_13);
		iText(1220,200,v[r][18],GLUT_BITMAP_8_BY_13);

		

		
	}
	if(format[r]==8)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1210,450,280,60);
		iFilledRectangle(1210,310,280,60);
		iFilledRectangle(1210,190,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1220,740,"Input the values of m,a,b,c:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,680,"m:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,540,"a:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,400,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,280,"c:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][19],GLUT_BITMAP_8_BY_13);
        iText(1220,460,v[r][20],GLUT_BITMAP_8_BY_13);
		iText(1220,320,v[r][21],GLUT_BITMAP_8_BY_13);
		iText(1220,200,v[r][22],GLUT_BITMAP_8_BY_13);



		
	}
	if(format[r]==9)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1210,450,280,60);
		iFilledRectangle(1210,310,280,60);
		iFilledRectangle(1210,190,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1220,740,"Input the values of m,a,b,c:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,680,"m:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,540,"a:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,400,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,280,"c:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][23],GLUT_BITMAP_8_BY_13);
        iText(1220,460,v[r][24],GLUT_BITMAP_8_BY_13);
		iText(1220,320,v[r][25],GLUT_BITMAP_8_BY_13);
		iText(1220,200,v[r][26],GLUT_BITMAP_8_BY_13);

		

		
	}
	if(format[r]==10)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1210,450,280,60);
		iFilledRectangle(1210,310,280,60);
		iFilledRectangle(1210,190,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1220,740,"Input the values of m,a,b,c:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,680,"m:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,540,"a:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,400,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,280,"c:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][27],GLUT_BITMAP_8_BY_13);
        iText(1220,460,v[r][28],GLUT_BITMAP_8_BY_13);
		iText(1220,320,v[r][29],GLUT_BITMAP_8_BY_13);
		iText(1220,200,v[r][30],GLUT_BITMAP_8_BY_13);


	}
	if(format[r]==11)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1210,450,280,60);
		iFilledRectangle(1210,310,280,60);
		iFilledRectangle(1210,190,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1220,740,"Input the values of m,a,b,c:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,680,"m:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,540,"a:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,400,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,280,"c:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][31],GLUT_BITMAP_8_BY_13);
        iText(1220,460,v[r][32],GLUT_BITMAP_8_BY_13);
		iText(1220,320,v[r][33],GLUT_BITMAP_8_BY_13);
		iText(1220,200,v[r][34],GLUT_BITMAP_8_BY_13);

		
	}
	if(format[r]==12)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1210,450,280,60);
		iFilledRectangle(1210,310,280,60);
		iFilledRectangle(1210,190,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1220,740,"Input the values of m,a,b,c:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,680,"m:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,540,"a:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,400,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,280,"c:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][35],GLUT_BITMAP_8_BY_13);
        iText(1220,460,v[r][36],GLUT_BITMAP_8_BY_13);
		iText(1220,320,v[r][37],GLUT_BITMAP_8_BY_13);
		iText(1220,200,v[r][38],GLUT_BITMAP_8_BY_13);

		
	}
	if(format[r]==13)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1210,450,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1220,740,"Input the values of a and b:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,680,"a:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,540,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][39],GLUT_BITMAP_8_BY_13);
        iText(1220,460,v[r][40],GLUT_BITMAP_8_BY_13);

		
	}
	if(format[r]==14)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1220,740,"Input the values of b:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,680,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][41],GLUT_BITMAP_8_BY_13);


	}
	if(format[r]==15)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1220,740,"Input the values of a:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,680,"a:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][42],GLUT_BITMAP_8_BY_13);


	}
	if(format[r]==16)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1220,740,"Input the values of a:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,680,"a:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][43],GLUT_BITMAP_8_BY_13);

		
	}
	if(format[r]==17)
	{
		iSetColor(164,260,164);
        iFilledRectangle(1210,730,280,60);
		iFilledRectangle(1210,590,280,60);
		iFilledRectangle(1210,450,280,60);
		iFilledRectangle(1310,30,50,50);
		iFilledRectangle(1210,30,50,30);
		iFilledRectangle(1210,110,190,50); ///////////add another function box
		iSetColor(0,0,0);
		iText(1220,740,"Input the values of a and b:",GLUT_BITMAP_TIMES_ROMAN_24);
        iText(1220,680,"a:",GLUT_BITMAP_HELVETICA_18);
        iText(1220,540,"b:",GLUT_BITMAP_HELVETICA_18);
		iText(1320,50,"Draw",GLUT_BITMAP_8_BY_13);
		iText(1215,40,"BACK",GLUT_BITMAP_9_BY_15);
		iText(1215,125,"Add another Function:",GLUT_BITMAP_HELVETICA_18);
		iText(1220,600,v[r][44],GLUT_BITMAP_8_BY_13);
        iText(1220,460,v[r][45],GLUT_BITMAP_8_BY_13);

		
	}
	
	
}

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
			
			if(x_diff<=10)
			{
				if(j%25==0)
				{
					iSetColor(0,0,0);
					iLine(x_axis+x_diff*j+6,-5000,x_axis+x_diff*j+6,5000);
					iLine(x_axis-x_diff*j,-5000,x_axis-x_diff*j,5000);
					iLine(-5000,y_axis+y_diff*j+6,5000,y_axis+y_diff*j+6);
					iLine(-5000,y_axis-y_diff*j,5000,y_axis-y_diff*j);
				}
			}
			
			
			
			else if(j%5){
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

	
    if(function[r]==0)
    {
        draw_menu();
    }
    else if(format[r]==0)
    {
        if(function[r]==1)
        {
            draw_linear_menu();
        }
        if(function[r]==2)
        {
            draw_polynomial_menu();
        }
        if(function[r]==3)
        {
            draw_trig_menu();
        }
        if(function[r]==4)
        {
            draw_exp_menu();
        }
        if(function[r]==5)
        {
            draw_log_menu();
        }
    }
    else 
    {
        take_inputs();
    }

	//show the function;;;;;;;;;;


	iSetColor(150,164,260);
	iFilledRectangle(0,400,250,800);
	iSetColor(255,255,255);
	iFilledRectangle(5,730,190,60);
	iFilledRectangle(5,660,190,60);
	iSetColor(0,0,0);
	iText(10,740,"YOUR FUNCTION:",GLUT_BITMAP_HELVETICA_18);
	
	

	
	
	//zoom buttons
	iSetColor(164,260,164);
	iFilledRectangle(1440,30,25,25);
	iFilledRectangle(1465,30,25,25);
	iSetColor(0,0,0);
	iText(1448,36,"+",GLUT_BITMAP_HELVETICA_18);
	iText(1448+25,36,"-",GLUT_BITMAP_HELVETICA_18);



	//printing the functions

	for(int h=0;h<10;h++)
	{

	


	if(draw[h])
	{
		if(format[h]==1)
		{
			char buffer[30];
			sprintf(buffer,"y=%.1fx+%.1f",var[h][1],var[h][2]);
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X=-10000,Y;X<=10000;X+=.5)
			{
				Y=(var[h][1]*(X-x_axis))+var[h][2]*(y_diff)+y_axis;
				iSetColor(0,0,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,5,100);
				}
			}
			
		}
		if(format[h]==2)
		{
			char buffer[30];
			sprintf(buffer,"y=%.1fx+%.1fy+%.1f",var[h][3],var[h][4],var[h][5]);
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X=-10000,Y;X<=10000;X+=.5)
			{
				Y=-(var[h][3]*(X-x_axis)+var[h][5]*y_diff)/var[h][4]+y_axis;
				iSetColor(0,0,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,5,100);
				}
			}
			
		}
		if(format[h]==3)
		{
			char buffer[30];
			sprintf(buffer,"y=x/%.1f+y/%.1f=1",var[h][6],var[h][7]);
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X=-10000,Y;X<=10000;X+=0.5)
			{
				Y=(y_diff-(X-x_axis)/var[h][6])*var[h][7]+y_axis;
				iSetColor(0,0,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,5,100);
				}
			}
			
		}
		if(format[h]==4)
		{
			char buffer[30];
			sprintf(buffer,"x=%.1f",var[h][8]);
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X,Y=-10000;Y<=10000;Y+=0.5)
			{
				X=x_axis+var[h][8]*x_diff;
				iSetColor(0,0,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,5,100);
				}
			}
			
		}
		if(format[h]==5)
		{
			char buffer[30];
			sprintf(buffer,"y=%.1fx^2 + %.1fx + %.1f",var[h][9],var[h][10],var[h][11]);
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X=-1000,Y;X<=1000;X+=0.01)
            {
                Y=var[h][9]*(pow((X-x_axis),2))/x_diff+var[h][10]*(X-x_axis)+var[h][11]*y_diff+y_axis;
                iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
            }
			
		}
		if(format[h]==6)
		{
			char buffer[30];
			sprintf(buffer,"x=%.1fy^2 + %.1fy + %.1f",var[h][12],var[h][13],var[h][14]);
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double Y=-1000,X;Y<=1000;Y+=0.01)
            {
                X=var[h][12]*(pow((Y-y_axis),2))/y_diff+var[h][13]*(Y-y_axis)+var[h][14]*y_diff+x_axis;
                iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
            }
			
		}
		// if(format==6)
		// {
		// 	char buffer[30];
		// 	sprintf(buffer,"x=%.1fy^2 + %.1fy + %.1f",var[12],var[13],var[14]);
		// 	iSetColor(0,0,0);
		// 	iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			
		// }
		if(format[h]==7)
		{
			char buffer[30];
			if(var[h][17]==0 && var[h][18]==0)
			sprintf(buffer,"y=%.1fsin(%.1fx)",var[h][15],var[h][16],var[h][17],var[h][18]);
			else if(var[h][18]==0) 
			sprintf(buffer,"y=%.1fsin(%.1fx+%.1f)",var[h][15],var[h][16],var[h][17]);
			else if(var[h][17]==0)
			sprintf(buffer,"y=%.1fsin(%.1fx)+%.1f",var[h][15],var[h][16],var[h][18]);

			else 
			{sprintf(buffer,"y=%.1fsin(%.1fx+%.1f)+%.1f",var[h][15],var[h][16],var[h][17],var[h][18]);}
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X=-20,Y;X<=1500;X+=0.05)
            {
                Y=(var[h][15]*sin((var[h][16]*(X-x_axis)/(x_diff)+var[h][17]*y_diff)/(2*PI))+var[h][18])*y_diff*10+y_axis;
                iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
            }
			
		}
		if(format[h]==8)
		{
			char buffer[30];
			if(var[h][21]==0 && var[h][22]==0)
			sprintf(buffer,"y=%.1fcos(%.1fx)",var[h][19],var[h][20],var[h][21],var[h][22]);
			else if(var[h][22]==0) 
			sprintf(buffer,"y=%.1fcos(%.1fx+%.1f)",var[h][19],var[h][20],var[h][21]);
			else if(var[h][21]==0)
			sprintf(buffer,"y=%.1fcos(%.1fx)+%.1f",var[h][19],var[h][20],var[h][22]);

			else 
			{sprintf(buffer,"y=%.1fcos(%.1fx+%.1f)+%.1f",var[h][19],var[h][20],var[h][21],var[h][22]);}
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X=-20,Y;X<=1500;X+=0.05)
            {
                Y=(var[h][19]*cos((var[h][20]*(X-x_axis)/(x_diff)+var[h][21]*y_diff)/(PI))+var[h][22])*y_diff*10+y_axis;
                iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
            }
			
		}
		if(format[h]==9)
		{
			char buffer[30];
			if(var[h][25]==0 && var[h][26]==0)
			sprintf(buffer,"y=%.1ftan(%.1fx)",var[h][23],var[h][24],var[h][25],var[h][26]);
			else if(var[h][26]==0) 
			sprintf(buffer,"y=%.1ftan(%.1fx+%.1f)",var[h][23],var[h][24],var[h][25]);
			else if(var[h][25]==0)
			sprintf(buffer,"y=%.1ftan(%.1fx)+%.1f",var[h][23],var[h][24],var[h][26]);

			else 
			{sprintf(buffer,"y=%.1ftan(%.1fx+%.1f)+%.1f",var[h][23],var[h][24],var[h][25],var[h][26]);}
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X=-20,Y;X<=1500;X+=0.05)
            {
                //if(((var[20]*(X-x_axis)/(x_diff)+var[21]*y_diff)/(PI))!=0 && (int)((var[20]*(X-x_axis)/(x_diff)+var[21]*y_diff))%90!=0)
				
				Y=(var[h][23]*tan((var[h][24]*(X-x_axis)/(x_diff)+var[h][25]*y_diff)/(2*PI))+var[h][26])*y_diff*10+y_axis;
                iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
				
            }
			
		}
		if(format[h]==10)
		{
			char buffer[30];
			if(var[h][29]==0 && var[h][30]==0)
			sprintf(buffer,"y=%.1fcot(%.1fx)",var[h][27],var[h][28],var[h][29],var[h][30]);
			else if(var[h][30]==0) 
			sprintf(buffer,"y=%.1fcot(%.1fx+%.1f)",var[h][27],var[h][28],var[h][29]);
			else if(var[h][29]==0)
			sprintf(buffer,"y=%.1fcot(%.1fx)+%.1f",var[h][27],var[h][28],var[h][30]);

			else 
			{sprintf(buffer,"y=%.1fcot(%.1fx+%.1f)+%.1f",var[h][27],var[h][28],var[h][29],var[h][30]);}
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X=-20,Y;X<=1500;X+=0.05)
            {
                //if(((var[20]*(X-x_axis)/(x_diff)+var[21]*y_diff)/(PI))!=0 && (int)((var[20]*(X-x_axis)/(x_diff)+var[21]*y_diff))%90!=0)
				
				Y=(var[h][27]* (1/tan((var[h][28]*(X-x_axis)/(x_diff)+var[h][29]*y_diff)/(2*PI)))+var[h][30])*y_diff*10+y_axis;
                iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
				
            }
			
		}
		if(format[h]==11)
		{
			char buffer[30];
			if(var[h][33]==0 && var[h][34]==0)
			sprintf(buffer,"y=%.1fcosec(%.1fx)",var[h][31],var[h][32],var[h][33],var[h][34]);
			else if(var[h][34]==0) 
			sprintf(buffer,"y=%.1fcosec(%.1fx+%.1f)",var[h][31],var[h][32],var[h][33]);
			else if(var[h][33]==0)
			sprintf(buffer,"y=%.1fcosec(%.1fx)+%.1f",var[h][31],var[h][32],var[h][34]);

			else 
			{sprintf(buffer,"y=%.1fcosec(%.1fx+%.1f)+%.1f",var[h][31],var[h][32],var[h][33],var[h][34]);}
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X=-20,Y;X<=1500;X+=0.05)
            {
                //if(((var[20]*(X-x_axis)/(x_diff)+var[21]*y_diff)/(PI))!=0 && (int)((var[20]*(X-x_axis)/(x_diff)+var[21]*y_diff))%90!=0)
				
				Y=(var[h][31]* (1/sin((var[h][32]*(X-x_axis)/(x_diff)+var[h][33]*y_diff)/(2*PI)))+var[h][34])*y_diff*10+y_axis;
                iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
				
            }
			
			
		}
		if(format[h]==12)
		{
			char buffer[30];
			if(var[h][37]==0 && var[h][38]==0)
			sprintf(buffer,"y=%.1fsec(%.1fx)",var[h][35],var[h][36],var[h][37],var[h][38]);
			else if(var[h][38]==0) 
			sprintf(buffer,"y=%.1fsec(%.1fx+%.1f)",var[h][35],var[h][36],var[h][37]);
			else if(var[h][37]==0)
			sprintf(buffer,"y=%.1fsec(%.1fx)+%.1f",var[h][35],var[h][36],var[h][38]);

			else 
			{sprintf(buffer,"y=%.1fsec(%.1fx+%.1f)+%.1f",var[h][35],var[h][36],var[h][37],var[h][38]);}
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X=-20,Y;X<=1500;X+=0.05)
            {
                //if(((var[20]*(X-x_axis)/(x_diff)+var[21]*y_diff)/(PI))!=0 && (int)((var[20]*(X-x_axis)/(x_diff)+var[21]*y_diff))%90!=0)
				
				Y=(var[h][35]* (1/cos((var[h][36]*(X-x_axis)/(x_diff)+var[h][37]*y_diff)/(2*PI)))+var[h][38])*y_diff*10+y_axis;
                iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
				
            }
			
			
		}
		if(format[h]==13)
		{
			char buffer[30];
			
			sprintf(buffer,"y=%.1lf^(%.1lfx)",var[h][39],var[h][40]);
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X=-20,Y;X<=1500;X+=0.05)
            {
                Y=pow(var[h][39],var[h][40]*(X-x_axis)/x_diff)*y_diff+y_axis+5;
				iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
            }	
		}
		if(format[h]==14)
		{
			char buffer[30];
			
			sprintf(buffer,"y=e^(%.1lfx)",var[h][41]);
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double X=-20,Y;X<=1500;X+=0.05)
            {
                Y=exp(var[h][41]*(X-x_axis)/x_diff)*y_diff+y_axis+5;
				iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
            }	
		}
		if(format[h]==15)
		{
			char buffer[30];
			
			sprintf(buffer,"y=log(%.1lfx)",var[h][42]);
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double Y=-1000,X;Y<=1500;Y+=0.05)
            {
				X=(pow(10,(Y-y_axis)/y_diff)*x_diff)/var[h][42]+x_axis;
				iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
            }	
		}
		if(format[h]==16)
		{
			char buffer[30];
			
			sprintf(buffer,"y=ln(%.1lfx)",var[h][43]);
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double Y=-1000,X;Y<=1500;Y+=0.05)
            {
				X=(pow(e,(Y-y_axis)/y_diff)*x_diff)/var[h][43]+x_axis;
				iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
            }	
		}
		if(format[h]==17)
		{
			char buffer[30];
			
			sprintf(buffer,"y=log%.1lf(%.1lfx)",var[h][44],var[h][45]);
			iSetColor(0,0,0);
			iText(10,670,buffer,GLUT_BITMAP_HELVETICA_18);
			for(double Y=-1000,X;Y<=1500;Y+=0.05)
            {
                X=(pow(var[h][44],(Y-y_axis)/y_diff)*x_diff)/var[h][45]+x_axis;
				iSetColor(0,255,0);
				if(X<=1200)
				{
					iFilledCircle(X,Y,2,100);
				}
            }
		}
		
	}
	}

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
	if(mx1>=0 && mx1<=1200)
    {
    
        mx_now=mx1;
        my_now=my1;
        x_axis_move=mx_now-mx_i;
        y_axis_move=my_now-my_i;
        //printf("x now %d y now %d\n x diff %d y diff %d",mx_now,my_now,x_axis_move,y_axis_move);
		printf("axes : %d %d\n",x_axis,y_axis);
        x_axis+=x_axis_move;
        y_axis+=y_axis_move;
        mx_i=mx_now;
        my_i=my_now;
    }
	
}

/*
	function iMouse() is called when the user presses/releases the mouse.
	(mx, my) is the position where the mouse pointer is.
	*/
void iMouse(int button, int state, int mx2, int my2) {
	if (button == GLUT_LEFT_BUTTON && state == GLUT_DOWN) {
		//place your codes here
		//printf("initial x = %d,initial y= %d\n",mx_i,my_i);
		if(mx2>=0 && mx2<=1200)
        {
        
            mx_i=mx2;
            my_i=my2;
            printf(" x initial %d y initial %d",mx_i,my_i);
        }
		if(mx2>=1440 && mx2<=1465 && my2>=30 && my2<=55)
		{
			
			
				x_diff+=5;
				y_diff+=5;
			
		}
		if(mx2>=1465 && mx2<=1490 && my2>=30 && my2<=55)
		{
			if(x_diff>=10)
			{
				x_diff-=5;
				y_diff-=5;
			}
		}
		if(function!=0 && mx2>=1210 && mx2<=1260 && my2>=30 && my2<=60)
		{
			//go_back=true;
		}
		


        if(function[r]==0)
        {
            if(mx2>=1210 && mx2<=1490 && my2>=660 && my2<=720)
            {
                function[r]=1;
				//for(int p=r+1;p<10;p++) function[p]=-1;
            }
            else if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
            {
                function[r]=2;
				//for(int p=r+1;p<10;p++) function[p]=-1;
            }
            else if(mx2>=1210 && mx2<=1490 && my2>=520 && my2<=580)
            {
                function[r]=3;
				//for(int p=r+1;p<10;p++) function[p]=-1;
            }
            else if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
            {
                function[r]=4;
				//for(int p=r+1;p<10;p++) function[p]=-1;
            }
            else if(mx2>=1210 && mx2<=1490 && my2>=380 && my2<=440)
            {
                function[r]=5;
				//for(int p=r+1;p<10;p++) function[p]=-1;
            }
            
        }
        else if(format[r]==0)
        {
            if(function[r]==1 && mx2>=1210 && mx2<=1490 && my2>=660 && my2<=720)
            {
                format[r]=1;
            }
            else if(function[r]==1 && mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
            {
                format[r]=2;
            }
            else if(function[r]==1 && mx2>=1210 && mx2<=1490 && my2>=520 && my2<=580)
            {
                format[r]=3;
            }
            else if(function[r]==1 && mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
            {
                format[r]=4;
            }
            else if(function[r]==2 && mx2>=1210 && mx2<=1490 && my2>=660 && my2<=720)
            {
                format[r]=5;
            }
            else if(function[r]==2 && mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
            {
                format[r]=6;
            }
            else if(function[r]==3 && mx2>=1210 && mx2<=1490 && my2>=660 && my2<=720)
            {
                format[r]=7;
            }
            else if(function[r]==3 && mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
            {
                format[r]=8;
            }
            else if(function[r]==3 && mx2>=1210 && mx2<=1490 && my2>=520 && my2<=580)
            {
                format[r]=9;
            }
            else if(function[r]==3 && mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
            {
                format[r]=10;
            }
            else if(function[r]==3 && mx2>=1210 && mx2<=1490 && my2>=380 && my2<=440)
            {
                format[r]=11;
            }
            else if(function[r]==3 && mx2>=1210 && mx2<=1490 && my2>=310 && my2<=370)
            {
                format[r]=12;
            }
            else if(function[r]==4 && mx2>=1210 && mx2<=1490 && my2>=660 && my2<=720)
            {
                format[r]=13;
            }
            else if(function[r]==4 && mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
            {
                format[r]=14;
            }
            else if(function[r]==5 && mx2>=1210 && mx2<=1490 && my2>=660 && my2<=720)
            {
                format[r]=15;
            }
            else if(function[r]==5 && mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
            {
                format[r]=16;
            }
            else if(function[r]==5 && mx2>=1210 && mx2<=1490 && my2>=450 && my2<=580)
            {
                format[r]=17;
            }
        }
		else 
		{
			if(format[r]==1)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][1]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][2]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==2)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][3]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][4]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=310 && my2<=370)
				{
					variable[r][5]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==3)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][6]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][7]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==4)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][8]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
            if(format[r]==5)
            {
                if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][9]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][10]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=310 && my2<=370)
				{
					variable[r][11]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
            }
			if(format[r]==6)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][12]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][13]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=310 && my2<=370)
				{
					variable[r][14]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==7)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][15]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][16]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=310 && my2<=370)
				{
					variable[r][17]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=170 && my2<=230)
				{
					variable[r][18]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==8)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][19]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][20]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=310 && my2<=370)
				{
					variable[r][21]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=170 && my2<=230)
				{
					variable[r][22]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==9)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][23]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][24]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=310 && my2<=370)
				{
					variable[r][25]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=170 && my2<=230)
				{
					variable[r][26]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==10)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][27]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][28]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=310 && my2<=370)
				{
					variable[r][29]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=170 && my2<=230)
				{
					variable[r][30]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==11)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][31]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][32]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=310 && my2<=370)
				{
					variable[r][33]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=170 && my2<=230)
				{
					variable[r][34]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==12)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][35]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][36]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=310 && my2<=370)
				{
					variable[r][37]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=170 && my2<=230)
				{
					variable[r][38]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==13)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][39]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][40]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==14)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][41]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==15)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][42]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==16)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][43]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
			if(format[r]==17)
			{
				if(mx2>=1210 && mx2<=1490 && my2>=590 && my2<=650)
				{
					variable[r][44]=true;
				}
				if(mx2>=1210 && mx2<=1490 && my2>=450 && my2<=510)
				{
					variable[r][45]=true;
				}
				if(mx2>=1310 && mx2<=1360 && my2>=30 && my2<=80)
				{
					draw[r]=true;
				}
			}
		}
    
    
    
    
    
    
    
    
    
    
    
    }

	//back button function
	if(mx2>=1210 && mx2<=1260 && my2>=30 && my2<=60)
	{
		// if(draw1)
		// {
		// 	if(format!=0) format=0,draw1=true;
		// 	else if(function!=0) function=0,draw1=true;
		// }
		r+=1;
	}
	
	

}
	// iFilledRectangle(1210,730,280,60);
    // iFilledRectangle(1210,660,280,60);
    // iFilledRectangle(1210,590,280,60);
    // iFilledRectangle(1210,520,280,60);
    // iFilledRectangle(1210,450,280,60);
    // iFilledRectangle(1210,380,280,60);
    // iFilledRectangle(1210,310,280,60);


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
	for(int p=1;p<50;p++)
	{
		if(variable[r][p])
		{
			int index=strlen(v[r][p]);
			if(key!='\r' && key!='\b')
			{
				v[r][p][index]=key;
				v[r][p][index+1]='\0';
			}
			else if(key=='\b')
			{
				v[r][p][index-1]='\0';
				index--;
			}
			else if(key=='\r')
			{
				variable[r][p]=false;
				var[r][p]=atof(v[r][p]);
			}
		}
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
	if(r==0) clear_variables;
	iInitialize(1500, 800, "project_trial_1");
	return 0;
}

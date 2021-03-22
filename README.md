# 2021.03.22

WEEK05

===========
01
----------
```C
#include <GL/glut.h> 
#include <stdio.h>
float teapotX=0,teapotY=0; ///茶壺的座標-1.0...+1.0
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glPushMatrix(); ///矩陣備份
        glTranslatef(teapotX,teapotY,0); ///照著座標移動
        glutSolidTeapot(0.3);
    glPopMatrix(); ///矩陣還原
    glEnd();
    glutSwapBuffers(); 
}

void motion (int x,int y)  ///mouse motion 的函式
{
    teapotX=(x-150)/150.0; ///座標換算
    teapotY=-(y-150)/150.0;
}
int main(int argc,char ** argv)
{
    glutInit(&argc,argv); 
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("08160554");
    glutDisplayFunc(display);  
    glutMotionFunc(motion); ///準備 mouse motion移動時的函式
    glutMainLoop(); 
}
```

02
----------

```C
#include <GL/glut.h>
#include <stdio.h>
float vx[2000],vy[2000];  ///準備一個頂點
int N=0;        ///有N個頂點
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glBegin(GL_LINE_LOOP);
    for(int i=0;i<N;i++)
    {
        glVertex2f(vx[i],vy[i]);
    }
    glEnd();
    glutSwapBuffers();
}
void mouse(int buttin,int state,int x,int y)
{

}
void motion (int x,int y)
{
    printf("%d %d\n",x,y);     ///把頂點記起來
    vx[N]=(x-150)/150.0;
    vy[N]=-(y-150)/150.0;
    N++;
    display();   ///要呼叫他才會畫圖
}        ///減一半再除一半，y加負號
int main(int argc,char ** argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("08160554");
    glutDisplayFunc(display);
    glutMouseFunc(mouse);      ///按下去彈起來
    glutMotionFunc(motion);    ///mouse motion 在動
    glutMainLoop();
}
```

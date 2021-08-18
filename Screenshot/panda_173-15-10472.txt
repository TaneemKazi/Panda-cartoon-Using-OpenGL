#include<windows.h>
#include <GL/glut.h>
#include <stdlib.h>
#include <math.h>

void init(void)
{
    glClearColor (0.5, 0.5, 0.5, 1);
    glOrtho      (0, 100.0, 0, 100.0, 0, 100.0);
}

void fullcircle(GLfloat rx, GLfloat ry, GLfloat x, GLfloat y)
{
    int i=0;
    float angle;
    GLfloat PI= 2.0f * 3.1416;
    glBegin(GL_TRIANGLE_FAN);
    glVertex2f(x,y);
    for(i=0; i<100; i++)
    {
        angle = 2 * PI * i/100;
        glVertex2f(x+(cos(angle)*rx),y+(sin(angle)* ry));
    }
    glEnd();
}

void halfcircleup(GLfloat rx, GLfloat ry, GLfloat x, GLfloat y)
{
    int i=0;
    float angle;
    GLfloat PI= 2.0f * 3.1416;
    glBegin(GL_TRIANGLE_FAN);
    glVertex2f(x,y);
    for(i=0; i<100; i++)
    {
        angle = 2 * PI * i/100;
        angle=angle/3.95;
        glVertex2f(x+(cos(angle)*rx),y+(sin(angle)* ry));
    }
    glEnd();
}

void halfcircledown(GLfloat rx, GLfloat ry, GLfloat x, GLfloat y)
{
    int i=0;
    float angle;
    GLfloat PI= 2.0f * 3.1416;
    glBegin(GL_TRIANGLE_FAN);
    glVertex2f(x,y);
    for(i=0; i<100; i++)
    {
        angle = 2 * PI * i/100;
        angle=angle/-3.95;
        glVertex2f(x+(cos(angle)*rx),y+(sin(angle)* ry));
    }
    glEnd();
}

void display(void)
{
    glClear(GL_COLOR_BUFFER_BIT| GL_DEPTH_BUFFER_BIT);

    //ear
    glColor3ub(0,0,0);
    fullcircle(5,5,35,84);
    fullcircle(5,5,65,84);

    glColor3ub(0,0,0);
    fullcircle(25,20,50,50);
    glColor3ub(255,255,255);
    fullcircle(18,12,50,73);

    //eye
    glColor3ub(0,0,0);
    fullcircle(4,5,45,75);
    fullcircle(4,5,55,75);

    glColor3ub(255,255,255);
    fullcircle(2,2,46,74);
    fullcircle(2,2,54,74);

    glColor3ub(0,0,0);
    fullcircle(1,1,46,74);
    fullcircle(1,1,54,74);

    //nose
    glBegin   (GL_POLYGON);
    glVertex2d(47,70);
    glVertex2d(54,70);
    glVertex2d(50.5,68);
    glEnd();

    //mouth
    glColor3f     (1,0,0);
    halfcircledown(3,1,50.5,67);

    //belly
    glColor3ub(255,255,255);
    glBegin   (GL_POLYGON);
    glVertex2d(30,56);
    glVertex2d(74,56);
    glVertex2d(68,40);
    glVertex2d(32,40);
    glEnd();

    fullcircle(5,10,29,48);
    fullcircle(5,10,70,48.5);

    //leg
    glColor3f (0,0,0);
    fullcircle(5,7,40,31);
    fullcircle(5,7,55,31);

    glColor3f (0,0,0);
    fullcircle(7,5,40,26);
    fullcircle(7,5,55,26);

    //hand
    fullcircle(4,10,28,49);
    fullcircle(4,10,71,50);

    glColor3f (1,1,1);
    fullcircle(19,6,50,39);

    glFlush();

}

int main()
{
    glutInitDisplayMode (GLUT_SINGLE | GLUT_RGB);
    glutInitWindowSize (500, 500);
    glutInitWindowPosition (750, 250);
    glutCreateWindow ("Panda Cartoon");
    init();
    glutDisplayFunc(display);
    glutMainLoop();
    return 0;
}

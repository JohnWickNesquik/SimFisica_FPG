# SimFisica_FPG
Hello World de Simuladores de Fisica, Donde un objeto en forma polygonal cae de cierta altura en la tierra.

##Link
https://github.com/JohnWickNesquik/SimFisica_FPG.git

##Conceptos

## Hola Mundo
Hace alusion a la emblematica forma de empezar en un nuevo mundo de programacion, en este caso programacion para Simular Fisicas. Este es considerado la primera experiencia dentro de la materia. 

##Gravedad en la tierra
Aqui tenemos como dato 9,807, pero que dentro del codigo sera dado por -10 por la conversion hecha por ingenieros, tambien en negativo para denotar la caida del cuerpo.

## Vector
un vector se cuenta a partir de un punto del espacio, tiene longitud que representa a escala una magnitud, contiene direccion determinada.

##Fixture
Se usan para describir el tamano, la forma y las propiedades de un objeto en la escena Fisica.

##Timestep
Se utiliza para determinar el intervalo de tiempo en el que se realiza una actualización en la
simulación para mantenerla estable.


##Codigo
#include <iostream>
#include <Box2d/Box2d.h>


int main(){

//Se define la gravedad, en la tierra.
    b2Vec2 gravity(0.0f, -10.0f);

    //Aqui definimos el mundo con la gravedad
    b2World world(gravity);

//Se define el cuerpo y su posicion
    b2BodyDef groundBodyDef;
    groundBodyDef.position.Set(0.0f, -10.0f);


//Se crea el cuerpo en el mundo
    b2Body* groundBody = world.CreateBody(&groundBodyDef);
//Se le da una forma de poligono y como una caja. 
    b2PolygonShape groundBox;
    groundBox.SetAsBox(50.0f, 10.0f);

    groundBody->CreateFixture(&groundBox, 0.0f);

    b2BodyDef bodyDef;
    bodyDef.type = b2_dynamicBody;
    bodyDef.position.Set(0.0f, 4.0f);
    b2Body* body = world.CreateBody(&bodyDef);

    b2PolygonShape dynamicBox;
    dynamicBox.SetAsBox(1.0f, 1.0f);

//Fixture donde se le da la forma, densidad y friccion
    b2FixtureDef fixtureDef;
    fixtureDef.shape = &dynamicBox;
    fixtureDef.density = 1.0f;
    fixtureDef.friction = 0.3f;

    body->CreateFixture(&fixtureDef);


    float timeStep = 1.0f / 60.0f;

    int32 velocityIterations = 6;
    int32 positionIterations = 2;

//Aqui el for actualizara posicion por posicion el movimiento
    for (int32 i = 0; i < 60; ++i)
    {
        world.Step(timeStep, velocityIterations, positionIterations);
        b2Vec2 position = body->GetPosition();
        float angle = body->GetAngle();
        printf("%4.2f %4.2f %4.2f\n", position.x, position.y, angle);
    }
}

# OpenGL-Ray-marching-dist-functions

Thoses functions are from the [iquilezles](http://www.dropwizard.io/1.0.2/docs/) article, and just stored here. Don't hesitate to have look on his blog, this guy did an amazing work !

## Primitives

### Sphere - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx00.png)

```
float sdSphere( vec3 p, float s )
{
  return length(p)-s;
}
```

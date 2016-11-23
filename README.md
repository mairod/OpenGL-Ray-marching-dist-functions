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

### Box - unsigned - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx01.png)

```
float udBox( vec3 p, vec3 b )
{
  return length(max(abs(p)-b,0.0));
}
```

### Round Box - unsigned - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx02.png)

```
float udRoundBox( vec3 p, vec3 b, float r )
{
  return length(max(abs(p)-b,0.0))-r;
}
```

### Box - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx03.png)

```
float sdBox( vec3 p, vec3 b )
{
  vec3 d = abs(p) - b;
  return min(max(d.x,max(d.y,d.z)),0.0) + length(max(d,0.0));
}
```

### Torus - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx04.png)

```
float sdTorus( vec3 p, vec2 t )
{
  vec2 q = vec2(length(p.xz)-t.x,p.y);
  return length(q)-t.y;
}
```

### Cylinder - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx05.png)

```
float sdCylinder( vec3 p, vec3 c )
{
  return length(p.xz-c.xy)-c.z;
}
```

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

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx01.png)

```
float sdBox( vec3 p, vec3 b )
{
  vec3 d = abs(p) - b;
  return min(max(d.x,max(d.y,d.z)),0.0) + length(max(d,0.0));
}
```

### Torus - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx03.png)

```
float sdTorus( vec3 p, vec2 t )
{
  vec2 q = vec2(length(p.xz)-t.x,p.y);
  return length(q)-t.y;
}
```

### Cylinder - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx04.png)

```
float sdCylinder( vec3 p, vec3 c )
{
  return length(p.xz-c.xy)-c.z;
}
```

### Cone - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx05.png)

```
float sdCone( vec3 p, vec2 c )
{
    // c must be normalized
    float q = length(p.xy);
    return dot(c,vec2(q,p.z));
}
```

### Plane - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx06.png)

```
float sdPlane( vec3 p, vec4 n )
{
  // n must be normalized
  return dot(p,n.xyz) + n.w;
}
```

### Hexagonal Prism - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx07.png)

```
float sdHexPrism( vec3 p, vec2 h )
{
    vec3 q = abs(p);
    return max(q.z-h.y,max((q.x*0.866025+q.y*0.5),q.y)-h.x);
}
```

### Triangular Prism - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx08.png)

```
float sdTriPrism( vec3 p, vec2 h )
{
    vec3 q = abs(p);
    return max(q.z-h.y,max(q.x*0.866025+p.y*0.5,-p.y)-h.x*0.5);
}
```

### Capsule / Line - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx09.png)

```
float sdCapsule( vec3 p, vec3 a, vec3 b, float r )
{
    vec3 pa = p - a, ba = b - a;
    float h = clamp( dot(pa,ba)/dot(ba,ba), 0.0, 1.0 );
    return length( pa - ba*h ) - r;
}
```

### Capped cylinder - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx10.png)

```
float sdCappedCylinder( vec3 p, vec2 h )
{
  vec2 d = abs(vec2(length(p.xz),p.y)) - h;
  return min(max(d.x,d.y),0.0) + length(max(d,0.0));
}
```

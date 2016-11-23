# OpenGL-Ray-marching-dist-functions

Thoses functions are from the [iquilezles](http://www.iquilezles.org/www/articles/distfunctions/distfunctions.htm) article, and just stored here. Don't hesitate to have look on his blog, this guy did an amazing work !

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

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx09.png)

```
float sdCone( vec3 p, vec2 c )
{
    // c must be normalized
    float q = length(p.xy);
    return dot(c,vec2(q,p.z));
}
```

### Plane - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx10.png)

```
float sdPlane( vec3 p, vec4 n )
{
  // n must be normalized
  return dot(p,n.xyz) + n.w;
}
```

### Hexagonal Prism - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx11.png)

```
float sdHexPrism( vec3 p, vec2 h )
{
    vec3 q = abs(p);
    return max(q.z-h.y,max((q.x*0.866025+q.y*0.5),q.y)-h.x);
}
```

### Triangular Prism - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx21.png)

```
float sdTriPrism( vec3 p, vec2 h )
{
    vec3 q = abs(p);
    return max(q.z-h.y,max(q.x*0.866025+p.y*0.5,-p.y)-h.x*0.5);
}
```

### Capsule / Line - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx22.png)

```
float sdCapsule( vec3 p, vec3 a, vec3 b, float r )
{
    vec3 pa = p - a, ba = b - a;
    float h = clamp( dot(pa,ba)/dot(ba,ba), 0.0, 1.0 );
    return length( pa - ba*h ) - r;
}
```

### Capped cylinder - signed - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx23.png)

```
float sdCappedCylinder( vec3 p, vec2 h )
{
  vec2 d = abs(vec2(length(p.xz),p.y)) - h;
  return min(max(d.x,d.y),0.0) + length(max(d,0.0));
}
```

### Capped Cone - signed - bound

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx26.png)

```
float sdCappedCone( in vec3 p, in vec3 c )
{
    vec2 q = vec2( length(p.xz), p.y );
    vec2 v = vec2( c.z*c.y/c.x, -c.z );
    vec2 w = v - q;
    vec2 vv = vec2( dot(v,v), v.x*v.x );
    vec2 qv = vec2( dot(v,w), v.x*w.x );
    vec2 d = max(qv,0.0)*qv/vv;
    return sqrt( dot(w,w) - max(d.x,d.y) ) * sign(max(q.y*v.x-q.x*v.y,w.y));
}
```

### Ellipsoid - signed - bound

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx25.png)

```
float sdEllipsoid( in vec3 p, in vec3 r )
{
    return (length( p/r ) - 1.0) * min(min(r.x,r.y),r.z);
}
```

### Triangle - unsigned - exact

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx24.png)

```
float dot2( in vec3 v ) { return dot(v,v); }
float udTriangle( vec3 p, vec3 a, vec3 b, vec3 c )
{
    vec3 ba = b - a; vec3 pa = p - a;
    vec3 cb = c - b; vec3 pb = p - b;
    vec3 ac = a - c; vec3 pc = p - c;
    vec3 nor = cross( ba, ac );

    return sqrt(
    (sign(dot(cross(ba,nor),pa)) +
     sign(dot(cross(cb,nor),pb)) +
     sign(dot(cross(ac,nor),pc))<2.0)
     ?
     min( min(
     dot2(ba*clamp(dot(ba,pa)/dot2(ba),0.0,1.0)-pa),
     dot2(cb*clamp(dot(cb,pb)/dot2(cb),0.0,1.0)-pb) ),
     dot2(ac*clamp(dot(ac,pc)/dot2(ac),0.0,1.0)-pc) )
     :
     dot(nor,pa)*dot(nor,pa)/dot2(nor) );
}
```

### Quad - unsigned - exact

```
float dot2( in vec3 v ) { return dot(v,v); }
float udQuad( vec3 p, vec3 a, vec3 b, vec3 c, vec3 d )
{
    vec3 ba = b - a; vec3 pa = p - a;
    vec3 cb = c - b; vec3 pb = p - b;
    vec3 dc = d - c; vec3 pc = p - c;
    vec3 ad = a - d; vec3 pd = p - d;
    vec3 nor = cross( ba, ad );

    return sqrt(
    (sign(dot(cross(ba,nor),pa)) +
     sign(dot(cross(cb,nor),pb)) +
     sign(dot(cross(dc,nor),pc)) +
     sign(dot(cross(ad,nor),pd))<3.0)
     ?
     min( min( min(
     dot2(ba*clamp(dot(ba,pa)/dot2(ba),0.0,1.0)-pa),
     dot2(cb*clamp(dot(cb,pb)/dot2(cb),0.0,1.0)-pb) ),
     dot2(dc*clamp(dot(dc,pc)/dot2(dc),0.0,1.0)-pc) ),
     dot2(ad*clamp(dot(ad,pd)/dot2(ad),0.0,1.0)-pd) )
     :
     dot(nor,pa)*dot(nor,pa)/dot2(nor) );
}
```

### Ellipsoid - signed - bound

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx25.png)

```
float sdEllipsoid( in vec3 p, in vec3 r )
{
    return (length( p/r ) - 1.0) * min(min(r.x,r.y),r.z);
}
```

# Operations

## Distance operations

### Union

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx05.png)

```
float opU( float d1, float d2 )
{
    return min(d1,d2);
}
```

### Substraction

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx06.png)

```
float opS( float d1, float d2 )
{
    return max(-d1,d2);
}
```

### Intersection

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx07.png)

```
float opI( float d1, float d2 )
{
    return max(d1,d2);
}
```

## Domain operations

### Repetition

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx12.png)

```
float opRep( vec3 p, vec3 c )
{
    vec3 q = mod(p,c)-0.5*c;
    return primitve( q );
}
```


### Rotation/Translation

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx13.png)

```
vec3 opTx( vec3 p, mat4 m )
{
    vec3 q = invert(m)*p;
    return primitive(q);
}
```

### Scale

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx14.png)

```
float opScale( vec3 p, float s )
{
    return primitive(p/s)*s;
}
```

# Deformations

## Distance deformations

### Displacement

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx15.png)

```
float opDisplace( vec3 p )
{
    float d1 = primitive(p);
    float d2 = displacement(p);
    return d1+d2;
}
```

### Blend

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx18.png)

```
float opBlend( vec3 p )
{
    float d1 = primitiveA(p);
    float d2 = primitiveB(p);
    return smin( d1, d2 );
}
```

## Domain deformations

### Twist

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx16.png)

```
float opTwist( vec3 p )
{
    float c = cos(20.0*p.y);
    float s = sin(20.0*p.y);
    mat2  m = mat2(c,-s,s,c);
    vec3  q = vec3(m*p.xz,p.y);
    return primitive(q);
}
```

### Cheap Bend

![alt tag](http://www.iquilezles.org/www/articles/distfunctions/gfx17.png)

```
float opCheapBend( vec3 p )
{
    float c = cos(20.0*p.y);
    float s = sin(20.0*p.y);
    mat2  m = mat2(c,-s,s,c);
    vec3  q = vec3(m*p.xy,p.z);
    return primitive(q);
}
```

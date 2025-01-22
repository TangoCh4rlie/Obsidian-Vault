```
void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    // Normalized pixel coordinates (from 0 to 1)
    vec2 uv = fragCoord/iResolution.xy;

    // Time varying pixel color
    vec3 col1 = vec3(1.,0.,0.);
    vec3 col2 = vec3(0.,0.,1.);
    
    vec3 col = col1*uv.x+(1.-uv.x)*col2;

    // Output to screen
    fragColor = vec4(col,1.0);
}
```

```
void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    // Normalized pixel coordinates (from 0 to 1)
    vec2 uv = fragCoord/iResolution.xy;

    // Time varying pixel color
    vec3 col1 = vec3(1.,0.,0.);
    vec3 col2 = vec3(0.,0.,1.);
    vec3 col3 = vec3(0.,1.,1.);
    vec3 col4 = vec3(0.,1.,0.);
    
    //vec3 col = col1*uv.x+(1.-uv.x)*col2;
    vec3 col = (1.-uv.x)*(1.-uv.y)*col1+uv.x*(1.-uv.y)*col2+(1.-uv.x)*uv.y*col3+uv.x*uv.y*col4;

	//ou solution du prof
	vec3 colA = col1*uv.x + (1.-uv.x)*col2;
    vec3 colB = col3*uv.x + (1.-uv.x)*col4;
	vec3 col = colA*uv.y + (1.-uv.y)*colB;

    // Output to screen
    fragColor = vec4(col,1.0);
}
```

```
void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    // Normalized pixel coordinates (from 0 to 1)
    vec2 uv = fragCoord/iResolution.xy;
    
    vec2 centre = iResolution.xy / 2.;
    
    float dist = distance(centre, fragCoord);
    
    float rayon = 300.;
    
    float alpha = dist/rayon;
    
    vec3 col1 = vec3(1.,0.,0.);
    vec3 col2 = vec3(0.,0.,1.);
    
    vec3 col = col1*alpha + (1.-alpha)*col2;
    
    fragColor = vec4(col,1.0);
}
```

```
void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    
    vec3 col1 = vec3(1.,0.,0.);
    vec3 col2 = vec3(0.,0.,1.);

    if (iMouse.z > 0.0) {
        vec2 centre = iResolution.xy / 2.;
        float dist = distance(centre, fragCoord);
        
        float rayon = 300.;
    
        float alpha = dist/rayon;
        
        vec3 col = col1*alpha + (1.-alpha)*col2;
        
        fragColor = vec4(col,1.0);
    } else {
     fragColor = vec4(col2,1.0);
    }
}
```

```
void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    
    vec3 col1 = vec3(1.,0.,0.);
    vec3 col2 = vec3(0.,0.,1.);

    if (iMouse.z > 0.0) {
        vec2 centre = iMouse.xy;
        float dist = distance(centre, fragCoord);
        
        float rayon = 300.;
    
        float alpha = dist/rayon;
        
        vec3 col = col1*alpha + (1.-alpha)*col2;
        
        fragColor = vec4(col,1.0);
    } else {
     fragColor = vec4(col2,1.0);
    } 
}
```

```
void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    
    vec3 col1 = vec3(1.,0.,0.);
    vec3 col2 = vec3(0.,0.,1.);

    if (iMouse.z > 0.0) {
        vec2 centre = iMouse.xy;
        float dist = distance(centre, fragCoord);
        
        float rayon = 300.;
        vec3 colA = col1;
    
        if (dist < rayon) {
            colA = col2;
        }
        
        fragColor = vec4(colA,1.0);
    } else {
     fragColor = vec4(col2,1.0);
    }
}
```

```
struct Sphere
{
    float radius;
    vec3 center;
    vec3 color;
};

struct Ray
{
    vec3 origin;
    vec3 direction;
};

struct It
{
    bool ok;  // presence ou non d'une intersection
    vec3 p;   // point d'intersection
    float t;  // distance d'intersection
    vec3 color; // couleur de l'intersection
    vec3 normal; // normal au point d'intersection
};

// renvoie t == 0 si pas d'intersection, sinon l'intersection
// est à ray.origin + t * ray.direction
float intersect(Sphere s, Ray r) {
    vec3 op = s.center - r.origin;
    float t;
    float eps = 1e-4;
    float b = dot(op, r.direction);
    float det = b * b - dot(op, op) + s.radius * s.radius;
    if(det < 0.0) return 0.0;
    else
    {
        det = sqrt(det);
        float t = b - det;
        if(t > eps)
            return t;
        else
        {
            t = b + det;
            if(t > eps)
                return t;
            else
                return 0.0;
        }
    }
}

// Compute smooth diffuse color
// normal : Normal vector
// lighting : Lighting vector
float Diffuse(in vec3 normal,in vec3 lighting)
{
  // Modified diffuse lighting
  float d = 0.5*(1.0+dot(normal,lighting));
  return d*d;
}

const int nbSpheres = 3;

It intersect_scene(Ray r)
{
    Sphere s[nbSpheres];

    // definition de la scene
    s[0].radius = 0.5;
    s[0].center = vec3(0.0, 0.0, 0.0);
    s[0].color = vec3(1.0, 1.0, 1.0);
    
    s[1].radius = 0.2;
    s[1].center = vec3(-1, 0.5, 0.0);
    s[1].color = vec3(0.0, 1.0, 1.0);
    
    s[2].radius = 0.5;
    s[2].center = vec3(0.4, -0.5, 1.0);
    s[2].color = vec3(0.0, 1.0, 0.0);


    // recherche d'une intersection
    It it;
    it.ok = false;

    for(int i = 0; i < nbSpheres; i++)
    {
        float t2 = intersect(s[i], r);

        // si intersection
        if(t2 != 0.0)
        {
            if(t2 < it.t || !it.ok)
            {
                it.ok = true;
                it.t = t2;

                // calcul de la position et de la normal
                it.p = r.origin + it.t * r.direction;
                it.color = s[i].color;
                it.normal = normalize(it.p - s[i].center);
            }
        }
    }

    return it;
}

void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    float ratio = iResolution.x / iResolution.y;
    vec2 uv = fragCoord.xy / iResolution.xy * 2.0 - 1.0;

    uv.x *= ratio;
    
    vec3 sun = vec3(-1.,-1.,-2.);

    Ray r;
    r.direction = vec3(0.0, 0.0, 1.0);
    r.origin = vec3(uv.xy, -1.0);

    It it = intersect_scene(r);
    
    if(it.ok)
    {
        float angle = dot(sun, it.normal);
        fragColor = vec4(angle*0.5*it.color, 1.0);

    }
    else
    {
        vec3 col1 =vec3(0.46,0.70,0.99);
        vec3 col2 =vec3(0.88,0.85,0.98);

        vec3 col = col1*uv.y+(1.-uv.y)*col2;
        fragColor = vec4(col,1.0);
    }

    
}


// carton
void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    float ratio = iResolution.x / iResolution.y;
    vec2 uv = fragCoord.xy / iResolution.xy * 2.0 - 1.0;

    uv.x *= ratio;
    
    vec3 sun = vec3(-1.,-1.,-2.);

    Ray r;
    r.direction = vec3(0.0, 0.0, 1.0);
    r.origin = vec3(uv.xy, -1.0);

    It it = intersect_scene(r);
    
    if(it.ok)
    {
        float angle = dot(sun, it.normal);
        if (angle > 2.3) {
            fragColor = vec4(0.8*it.color, 1.0);
        } else if (angle < 0.8) {
            fragColor = vec4(0.2*it.color, 1.0);
        } else {
            fragColor = vec4(0.5*it.color, 1.0);
        }

    }
    else
    {
        vec3 col1 =vec3(0.46,0.70,0.99);
        vec3 col2 =vec3(0.88,0.85,0.98);

        vec3 col = col1*uv.y+(1.-uv.y)*col2;
        fragColor = vec4(col,1.0);
    }

    
}
```

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
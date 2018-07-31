function int FRAC(float x0, y0, z0; int imax){
    float x, y; z, xnew, ynew, znew, n=ch('n'), r, theta, phi;
    int i;
    
    x = x0;
    y = y0;
    z = z0;
    
    for(i=0; i < imax; i++){
                
        r = sqrt(x*x + y*y + z*z);
        theta = atan2(sqrt(x*x + y*y) , z);
        phi = atan2(y,x);
        
        xnew = pow(r, n) * sin(theta*n) * cos(phi*n) + x0;
        ynew = pow(r, n) * sin(theta*n) * sin(phi*n) + y0;
        znew = pow(r, n) * cos(theta*n) + z0;
        
        if(xnew*xnew + ynew*ynew + znew*znew > 8){
            return(i);
        }
        
        x = xnew;
        y = ynew;
        z = znew;
    }
    return(imax);
}


//--- Main ---

int maxiter = 8;

if(FRAC(@P.x, @P.y, @P.z, maxiter) < maxiter){
    @density = 0.0;
}
else {
    @density = 1.0;
}

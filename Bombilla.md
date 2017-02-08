# Codigos
package ejemplobombilla;

/**
 *
 */
public class bombilla {
    private boolean estado = false;
    
    public bombilla (){
    estado = false;
            }
    
    public void encender () {
    this.estado = true;
    }
     public void apagar () {
     this.estado = false;
     }   
     public void consultarEstado() {
     if (estado = true)
         System.out.println("Encendida");
     else
         System.out.println("Apagada");
     }
}

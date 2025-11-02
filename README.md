# 1-herencia
/**
 * SISTEMA DE GESTIÓN DE ESTUDIANTES CON HERENCIA
 * Actividad Formativa 3
 * Todas las clases en un solo archivo
 */

// 1. CLASE BASE
class Estudiante {
    protected String nombre;
    protected String id;
    protected int edad;
    protected String carrera;
    protected double[] calificaciones;
    
    public Estudiante() {
        this.nombre = "";
        this.id = "";
        this.edad = 0;
        this.carrera = "";
        this.calificaciones = new double[0];
    }
    
    public Estudiante(String nombre, String id, int edad, String carrera) {
        this.nombre = nombre;
        this.id = id;
        this.edad = edad;
        this.carrera = carrera;
        this.calificaciones = new double[0];
    }
    
    public double calcularPromedio() {
        if (calificaciones.length == 0) return 0.0;
        
        double suma = 0;
        for (double calificacion : calificaciones) {
            suma += calificacion;
        }
        return suma / calificaciones.length;
    }
    
    public boolean estaAprobado() {
        return calcularPromedio() >= 6.0;
    }
    
    public void mostrarInformacion() {
        System.out.println("Nombre: " + nombre);
        System.out.println("ID: " + id);
        System.out.println("Carrera: " + carrera);
        System.out.println("Promedio: " + String.format("%.2f", calcularPromedio()));
    }
    
    public String getNombre() { return nombre; }
    public void setNombre(String nombre) { this.nombre = nombre; }
    public String getId() { return id; }
    public void setId(String id) { this.id = id; }
    public int getEdad() { return edad; }
    public void setEdad(int edad) { this.edad = edad; }
    public String getCarrera() { return carrera; }
    public void setCarrera(String carrera) { this.carrera = carrera; }
    public double[] getCalificaciones() { return calificaciones; }
    public void setCalificaciones(double[] calificaciones) { 
        this.calificaciones = calificaciones; 
    }
}

// 2. CLASE DERIVADA - Estudiante Internacional
class EstudianteInternacional extends Estudiante {
    private String paisOrigen;
    private String visaEstudio;
    
    public EstudianteInternacional(String nombre, String id, int edad, 
                                 String carrera, String paisOrigen) {
        super(nombre, id, edad, carrera);
        this.paisOrigen = paisOrigen;
        this.visaEstudio = "Pendiente";
    }
    
    @Override
    public void mostrarInformacion() {
        super.mostrarInformacion();
        System.out.println("País Origen: " + paisOrigen);
        System.out.println("Visa: " + visaEstudio);
        System.out.println("Tipo: Internacional");
        System.out.println("-----------------------------");
    }
    
    public String getPaisOrigen() { return paisOrigen; }
    public void setPaisOrigen(String paisOrigen) { this.paisOrigen = paisOrigen; }
    public String getVisaEstudio() { return visaEstudio; }
    public void setVisaEstudio(String visaEstudio) { this.visaEstudio = visaEstudio; }
}

// 3. CLASE DERIVADA - Estudiante Becado
class EstudianteBecado extends Estudiante {
    private String tipoBeca;
    private double porcentajeBeca;
    
    public EstudianteBecado(String nombre, String id, int edad, 
                          String carrera, String tipoBeca, double porcentajeBeca) {
        super(nombre, id, edad, carrera);
        this.tipoBeca = tipoBeca;
        this.porcentajeBeca = porcentajeBeca;
    }
    
    @Override
    public boolean estaAprobado() {
        return calcularPromedio() >= 7.0;
    }
    
    @Override
    public void mostrarInformacion() {
        super.mostrarInformacion();
        System.out.println("Tipo Beca: " + tipoBeca);
        System.out.println("Porcentaje Beca: " + porcentajeBeca + "%");
        System.out.println("Estado: " + (estaAprobado() ? "BECA ACTIVA" : "BECA EN RIESGO"));
        System.out.println("-----------------------------");
    }
    
    public String getTipoBeca() { return tipoBeca; }
    public void setTipoBeca(String tipoBeca) { this.tipoBeca = tipoBeca; }
    public double getPorcentajeBeca() { return porcentajeBeca; }
    public void setPorcentajeBeca(double porcentajeBeca) { 
        this.porcentajeBeca = porcentajeBeca; 
    }
}

// 4. CLASE PRINCIPAL
public class Main {
    public static void main(String[] args) {
        System.out.println("=== ACTIVIDAD 3 - SISTEMA CON HERENCIA ===");
        
        // Crear estudiantes de diferentes tipos
        Estudiante regular = new Estudiante("Ana García", "2024001", 20, "Sistemas");
        regular.setCalificaciones(new double[]{8.0, 7.5, 9.0});
        
        EstudianteInternacional internacional = new EstudianteInternacional(
            "John Smith", "2024002", 22, "Administración", "Estados Unidos"
        );
        internacional.setCalificaciones(new double[]{9.0, 8.5, 9.5});
        
        EstudianteBecado becado = new EstudianteBecado(
            "María López", "2024003", 19, "Medicina", "Excelencia Académica", 80.0
        );
        becado.setCalificaciones(new double[]{6.5, 7.0, 6.0});
        
        // Array polimórfico - demostración de herencia
        Estudiante[] estudiantes = {regular, internacional, becado};
        
        // Mostrar información de todos los estudiantes
        System.out.println("\n--- INFORMACIÓN DE ESTUDIANTES ---");
        for (Estudiante est : estudiantes) {
            est.mostrarInformacion();
        }
        
        // Verificar estados académicos
        System.out.println("--- ESTADOS ACADÉMICOS ---");
        for (Estudiante est : estudiantes) {
            String tipo = est.getClass().getSimpleName();
            System.out.println(tipo + " - " + est.getNombre() + 
                             ": " + (est.estaAprobado() ? "APROBADO" : "REPROBADO"));
        }
        
        System.out.println("\n=== FIN DEL SISTEMA ===");
    }
}

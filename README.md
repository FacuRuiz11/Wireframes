erDiagram
    USUARIO ||--o{ PAAC : "crea"
    DEPARTAMENTO ||--o{ MATERIA : "contiene"
    MATERIA ||--o{ PAAC : "tiene"
    PAAC ||--o{ UNIDAD : "contiene"
    PAAC ||--o{ TRABAJO_PRACTICO : "contiene"
    PAAC ||--o{ COMENTARIO : "recibe"
    PAAC ||--o{ EQUIPO_CATEDRA : "tiene"
    PAAC ||--o{ RECURSO_DIDACTICO : "utiliza"
    PAAC ||--o{ TIPO_EVALUACION : "define"
    PAAC ||--o{ METODOLOGIA_EVALUACION : "define"
    PAAC ||--o{ ESTADO : "tiene"
    PAAC ||--o{ RESOLUCION : "tiene"
    TRABAJO_PRACTICO ||--o{ METODO_EVALUACION : "tiene"
    UNIDAD ||--o{ TRABAJO_PRACTICO : "asociado"

    USUARIO {
        int id PK
        string nombre
        string apellido
        string email
        string password
        enum rol "Profesor, UP, DC, Admin, Personal"
        int departamento_id FK
    }
    
    DEPARTAMENTO {
        int id PK
        string nombre
        int sede_id FK
    }
    
    SEDE {
        int id PK
        string nombre
    }
    
    MATERIA {
        int id PK
        string nombre
        string plan_estudio
        int creditos_horarios
        enum regimen "Cuatrimestral, Anual"
        text contenidos_minimos
        int departamento_id FK
    }
    
    PAAC {
        int id PK
        int año
        date fecha_presentacion
        date fecha_limite_correccion
        int materia_id FK
        int usuario_id FK
        text importancia_asignatura
        text perfil_profesional
        text articulacion_correlativas
        text articulacion_mismo_anio
        text analisis_alumnos
        text infraestructura
        text objetivos_carrera
        text objetivos_catedra
        text objetivos_especificos
        text descripcion_modelo_evaluacion
        text criterios_evaluacion
        text bibliografia_basica
        text bibliografia_complementaria
        text regimen_aprobacion_promocionales
        text regimen_aprobacion_regulares
        text regimen_aprobacion_libres
    }
    
    UNIDAD {
        int id PK
        string titulo
        text descripcion
        int orden
        int paac_id FK
    }
    
    TRABAJO_PRACTICO {
        int id PK
        string titulo
        text proposito
        text contenido
        text actividad
        string ubicacion
        string epoca_realizacion
        enum tipo "Regular, Laboratorio, Campo"
        int unidad_id FK
        int paac_id FK
    }
    
    METODO_EVALUACION {
        int id PK
        string descripcion
        int trabajo_practico_id FK
    }
    
    EQUIPO_CATEDRA {
        int id PK
        string nombre
        enum tipo "Titular, Asociado, Adjunto, JTP, Ayudante, Adscripto, AyudanteAlumno"
        int paac_id FK
    }
    
    RECURSO_DIDACTICO {
        int id PK
        string nombre
        enum tipo "GuiaEjercicios, GuiaTP, Apuntes, Videos, Presentaciones, Bibliografia, SoporteInformatico, Otro"
        int paac_id FK
    }
    
    TIPO_EVALUACION {
        int id PK
        enum tipo "Inicial, Proceso, Final"
        int paac_id FK
    }
    
    METODOLOGIA_EVALUACION {
        int id PK
        string nombre
        enum tipo "OralIndividual, OralGrupal, EscritaIndividual, EscritaGrupal, Informes, Otra"
        int paac_id FK
    }
    
    COMENTARIO {
        int id PK
        text contenido
        date fecha
        string campo_referencia
        text respuesta
        boolean corregido
        int usuario_id FK
        int paac_id FK
    }
    
    ESTADO {
        int id PK
        enum estado "Borrador, Presentado, Verificación, Corregido, PendienteAprobación, Aprobado, NoCumplimiento"
        date fecha_cambio
        int paac_id FK
    }
    
    RESOLUCION {
        int id PK
        string numero
        date fecha
        int usuario_id FK
        int paac_id FK
    }

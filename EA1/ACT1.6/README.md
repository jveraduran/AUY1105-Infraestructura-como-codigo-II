# AUY1105 - INFRAESTRUCTURA COMO CÓDIGO II

# USO DE HERRAMIENTAS PARA CUMPLIMIENTOS DE SEGURIDAD

## DESARROLLO DE ACTIVIDAD

### 1. Iniciar el Laboratorio Learner Lab en AWS Academy

1. Accede a **AWS Academy** y selecciona el curso correspondiente.  
2. Inicia el laboratorio Learner Lab haciendo clic en **Start Lab**.  
3. Accede a la consola de AWS utilizando las credenciales temporales proporcionadas.

### 2. Crear una Instancia EC2

1. En la consola de AWS, ve al servicio **EC2**.  
2. Haz clic en **Launch Instance** y configura los siguientes parámetros:
   - Nombre: `Infraestructura-Actividad`
   - Tipo de instancia: `t2.micro` (o el disponible en el lab)
   - AMI: **Amazon Linux 2**
   - Configura el almacenamiento y revisa las reglas de seguridad (permitir SSH, puerto 22).  

3. Haz clic en **Launch** y selecciona o crea un par de claves para conectarte.

### 3. Conectarse a la Instancia EC2

1. Una vez que la instancia esté corriendo, haz clic en **Connect** y sigue las instrucciones para conectarte mediante SSH.  
2. Usa el siguiente comando (ajustando el archivo de clave):

```bash
   ssh -i "nombre-de-tu-clave.pem" ec2-user@<dirección-ip-pública>
```

### 4. Subir y Ejecutar el Script install.sh
1. Sube el archivo a la instancia EC2:

```bash
   scp -i "nombre-de-tu-clave.pem" install.sh ec2-user@<dirección-ip-pública>:~
```

2. Conéctate nuevamente a la instancia y ejecuta el script:

```bash
chmod +x install.sh
./install.sh
```

### 5. Ejecutar código Terraform

1. Ejecuta el comando para inicializar el entorno de Terraform y descargar los providers necesarios.

```bash
terraform init
```

2. Exportar las Credenciales de AWS 
```bash
export AWS_ACCESS_KEY_ID=<tu_access_key_id>
export AWS_SECRET_ACCESS_KEY=<tu_secret_access_key>
export AWS_SESSION_TOKEN=<tu_session_token>
```

3. Generar el Plan de Terraform en Formato Binario
```bash
terraform plan -out=tfplan
```

4. Convertir el Plan Binario a Formato JSON
```bash
terraform show -json tfplan > tfplan.json
```

5. Ejecutar validación de seguridad en código Terraform
```bash
checkov -f tfplan.json
```

## REFLEXIONES

- Importancia de la Seguridad por Diseño: La actividad resalta cómo la seguridad debe integrarse desde el inicio en los procesos de IaC. Los errores comunes como claves expuestas o configuraciones incorrectas pueden ser detectados a tiempo.

- Automatización y consistencia: Utilizar herramientas como Terraform y Checkov automatiza la validación de la infraestructura, asegurando consistencia en la aplicación de buenas prácticas de seguridad.

- Colaboración y mejora continua: Fomentar la cultura DevSecOps, donde todos los involucrados en el desarrollo y la operación están comprometidos con la seguridad, es clave para una infraestructura robusta.

- Uso práctico de la nube y IaC: Conectar estos conceptos con casos reales prepara a los estudiantes para enfrentar escenarios del mundo laboral, alineados con estándares de seguridad de la industria.
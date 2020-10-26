# Creación de "n" instancias EC2 tipo ubuntu en AWS usando Terraform

Script en Terraform que automatiza el despliegue en AWS n instancias EC2 tipo ubuntu con acceso a internet que permiten tráfico SSH, HTTP y HTTPS

## 1. Configura AWS (este script corre en la región "us-west-2")
Antes de ejecutar este script, ejecuta `aws configure` para habilitar
   - AWS Access Key ID
   - AWS Secret Access Key
   - Default region name 
   - Default output format (json,yaml,yaml-stream,text,table)

## 2. Genera un par de llaves rsa pública/privada
   ```bash 
   ssh-keygen
   ```
   Sálvala en el directorio donde correras este script `<ruta_absoluta>/key`, deja vacío `passphrase`

## 3. Conexión por SSH a la máquina virtual 
   ```bash
   ssh -v -l ubuntu -i linux-training-key <ip_publica_instancia_ec2>
   ```
## 4. Script compatible con la versión de Terraform v0.11.3, estos son los pasos para descargarlo e instalarlo
   ```bash
  wget https://releases.hashicorp.com/terraform/0.11.3/terraform_0.11.3_linux_amd64.zip
  unzip terraform_0.13.3_linux_amd64.zip
  sudo mv terraform /usr/local/bin/
  terraform --version 
   ```

## 5. Para ejecutar el script `terraform apply -var "nombre_instancia=<nombre_recursos>" -var "cantidad_instancias=<n>"` cuando el siguiente mensaje aparezca, escribe `yes`:
   ```bash
   Do you want to perform these actions?
     Terraform will perform the actions described above.
     Only 'yes' will be accepted to approve.

     Enter a value:
   ```

Una vez el script se ejecuta generará un mensaje parecido a esto:

   ```bash
   Apply complete! Resources: <cantidad_recursos> added, 0 changed, 0 destroyed.
   ```

## 6. Para eliminar la infraestructura desplegada, ejecuta `terraform destroy` y cuando aparezca el siguiente mensaje, escribe `yes`:
   ```bash
   Do you really want to destroy?
     Terraform will destroy all your managed infrastructure, as shown above.
     There is no undo. Only 'yes' will be accepted to confirm.

     Enter a value:
   ```

El script una vez ejecutado generará un mensaje parecido a esto:

   ```bash
   Destroy complete! Resources: <cantidad_recursos> destroyed.
   ```

## 7. Valida en el portal de AWS que los recursos se hayan eliminado
Las instancias EC2 deberan aparecen con estado `Terminated` y después de algunos minutos desaparecerán de la consola

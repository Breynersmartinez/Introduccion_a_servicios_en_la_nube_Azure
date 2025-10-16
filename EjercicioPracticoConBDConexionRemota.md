
##  Arquitectura del Sistema

- **VM1 (Servidor)**: Spring Boot + conexion a DB en la nube  PostgreSQL con contenedor Docker
- **VM2 (Cliente)**: Aplicación cliente que consume la API

##  PARTE 1: Configuración de VM1 (Servidor)

### 1.1 Preparar la VM Ubuntu 22.04 LTS

```bash
# Actualizar el sistema
sudo apt update && sudo apt upgrade -y

# Instalar dependencias necesarias
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

### 1.2 Instalar Docker y Docker Compose

```bash
# Instalar Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

# Agregar tu usuario al grupo docker
sudo usermod -aG docker $USER
newgrp docker

# Verificar instalación
docker --version
docker compose version
```

### 1.3 Crear la Estructura del Proyecto

```bash
# Crear directorio del proyecto
mkdir ~/spring-products-crud
cd ~/spring-products-crud

# Crear estructura de directorios
mkdir -p src/main/java/com/example/products/{controller,service,repository,model,config}
mkdir -p src/main/resources
```

### 1.4 Crear el proyecto Spring Boot

**Archivo: `pom.xml`**

```bash
cat > pom.xml << 'EOF'
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.2.0</version>
        <relativePath/>
    </parent>
    
    <groupId>com.example</groupId>
    <artifactId>products-crud</artifactId>
    <version>1.0.0</version>
    <name>Products CRUD</name>
    
    <properties>
        <java.version>17</java.version>
    </properties>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <scope>runtime</scope>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
    </dependencies>
    
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
EOF
```

**Archivo: `src/main/resources/application.properties`**

```bash
cat > src/main/resources/application.properties << 'EOF'
spring.datasource.url=${SPRING_DATASOURCE_URL}
spring.datasource.username=${SPRING_DATASOURCE_USERNAME}
spring.datasource.password=${SPRING_DATASOURCE_PASSWORD}
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.datasource.url=${SPRING_DATASOURCE_URL}
spring.datasource.username=${SPRING_DATASOURCE_USERNAME}
spring.datasource.password=${SPRING_DATASOURCE_PASSWORD}
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
EOF
```


# Enfoques de modelado en JPA

| Enfoque            | Qué se hace  primero                              | 
| ------------------ | ------------------------------------------------- | 
| **Code-First**     | Creas las entidades y JPA genera la base de datos | 
| **Database-First** | Ya tienes la base y mapeas las entidades          |


# EXPLICACION DEL FUNCIONAMIENTO DE JPA:

##  spring.jpa.hibernate.ddl-auto=update, Hibernate:

- Crea las tablas si no existen.

- Las actualiza si cambias la estructura de las entidades.

- No borra datos existentes.

##  create, Hibernate:

- Borra las tablas y las vuelve a crear cada vez que inicias la app.

##  create-drop, Hibernate:

- Crea las tablas al iniciar y las borra al detener la app.

##  validate, Hibernate:

- Solo verifica que las tablas existan y coincidan con las entidades (no crea ni modifica nada).


### 1.5 Crear las Clases Java

**Archivo: `src/main/java/com/example/products/ProductsApplication.java`**

```bash
cat > src/main/java/com/example/products/ProductsApplication.java << 'EOF'
package com.example.products;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class ProductsApplication {
    public static void main(String[] args) {
        SpringApplication.run(ProductsApplication.class, args);
    }
}
EOF
```

**Archivo: `src/main/java/com/example/products/model/Product.java`**

```bash
cat > src/main/java/com/example/products/model/Product.java << 'EOF'
package com.example.products.model;

import jakarta.persistence.*;
import jakarta.validation.constraints.*;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
import java.math.BigDecimal;
import java.time.LocalDateTime;

@Entity
@Table(name = "products")
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Product {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @NotBlank(message = "El nombre es obligatorio")
    @Size(min = 3, max = 100, message = "El nombre debe tener entre 3 y 100 caracteres")
    @Column(nullable = false, length = 100)
    private String name;
    
    @Size(max = 500, message = "La descripción no puede exceder 500 caracteres")
    @Column(length = 500)
    private String description;
    
    @NotNull(message = "El precio es obligatorio")
    @DecimalMin(value = "0.01", message = "El precio debe ser mayor a 0")
    @Column(nullable = false, precision = 10, scale = 2)
    private BigDecimal price;
    
    @Min(value = 0, message = "El stock no puede ser negativo")
    @Column(nullable = false)
    private Integer stock = 0;
    
    @Column(name = "created_at", nullable = false, updatable = false)
    private LocalDateTime createdAt;
    
    @Column(name = "updated_at")
    private LocalDateTime updatedAt;
    
    @PrePersist
    protected void onCreate() {
        createdAt = LocalDateTime.now();
        updatedAt = LocalDateTime.now();
    }
    
    @PreUpdate
    protected void onUpdate() {
        updatedAt = LocalDateTime.now();
    }
}
EOF
```

**Archivo: `src/main/java/com/example/products/repository/ProductRepository.java`**

```bash
cat > src/main/java/com/example/products/repository/ProductRepository.java << 'EOF'
package com.example.products.repository;

import com.example.products.model.Product;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;
import java.util.List;

@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
    List<Product> findByNameContainingIgnoreCase(String name);
    List<Product> findByStockGreaterThan(Integer stock);
}
EOF
```

**Archivo: `src/main/java/com/example/products/service/ProductService.java`**

```bash
cat > src/main/java/com/example/products/service/ProductService.java << 'EOF'
package com.example.products.service;

import com.example.products.model.Product;
import com.example.products.repository.ProductRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;
import java.util.List;
import java.util.Optional;

@Service
@Transactional
public class ProductService {
    
    
    private final ProductRepository productRepository;
    public ProductService(ProductRepository productRepository){
    this.productRepository = productRepository;
    }

    
    public List<Product> getAllProducts() {
        return productRepository.findAll();
    }
    
    public Optional<Product> getProductById(Long id) {
        return productRepository.findById(id);
    }
    
    public Product createProduct(Product product) {
        return productRepository.save(product);
    }
    
    public Product updateProduct(Long id, Product productDetails) {
        Product product = productRepository.findById(id)
            .orElseThrow(() -> new RuntimeException("Producto no encontrado con id: " + id));
        
        product.setName(productDetails.getName());
        product.setDescription(productDetails.getDescription());
        product.setPrice(productDetails.getPrice());
        product.setStock(productDetails.getStock());
        
        return productRepository.save(product);
    }
    
    public void deleteProduct(Long id) {
        Product product = productRepository.findById(id)
            .orElseThrow(() -> new RuntimeException("Producto no encontrado con id: " + id));
        productRepository.delete(product);
    }
    
    public List<Product> searchByName(String name) {
        return productRepository.findByNameContainingIgnoreCase(name);
    }
}
EOF
```

**Archivo: `src/main/java/com/example/products/controller/ProductController.java`**

```bash
cat > src/main/java/com/example/products/controller/ProductController.java << 'EOF'
package com.example.products.controller;

import com.example.products.model.Product;
import com.example.products.service.ProductService;
import jakarta.validation.Valid;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;
import java.util.List;

@RestController
@RequestMapping("/api/products")
@CrossOrigin(origins = "*")
public class ProductController {
    
    
    private final ProductService productService;
    public ProductController(ProductService productService){
    this.productService = productService;
    }
    
    @GetMapping
    public ResponseEntity<List<Product>> getAllProducts() {
        return ResponseEntity.ok(productService.getAllProducts());
    }
    
    @GetMapping("/{id}")
    public ResponseEntity<Product> getProductById(@PathVariable Long id) {
        return productService.getProductById(id)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
    }
    
    @PostMapping
    public ResponseEntity<Product> createProduct(@Valid @RequestBody Product product) {
        Product createdProduct = productService.createProduct(product);
        return ResponseEntity.status(HttpStatus.CREATED).body(createdProduct);
    }
    
    @PutMapping("/{id}")
    public ResponseEntity<Product> updateProduct(
            @PathVariable Long id, 
            @Valid @RequestBody Product product) {
        try {
            Product updatedProduct = productService.updateProduct(id, product);
            return ResponseEntity.ok(updatedProduct);
        } catch (RuntimeException e) {
            return ResponseEntity.notFound().build();
        }
    }
    
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteProduct(@PathVariable Long id) {
        try {
            productService.deleteProduct(id);
            return ResponseEntity.noContent().build();
        } catch (RuntimeException e) {
            return ResponseEntity.notFound().build();
        }
    }
    
    @GetMapping("/search")
    public ResponseEntity<List<Product>> searchProducts(@RequestParam String name) {
        return ResponseEntity.ok(productService.searchByName(name));
    }
}
EOF
```

### 1.6 Crear el Dockerfile

```bash
cat > Dockerfile << 'EOF'
FROM maven:3.9-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
EOF
```

### 1.7 Crear docker-compose.yml

## CONEXION RENDER
```bash
services:
  springboot-app:
    build: .
    container_name: products-api
    ports:
      - "8080:8080"
    environment:
      SPRING_DATASOURCE_URL: jdbc:postgresql://dpg-d3nuunali9vc73ch4tb0-a.oregon-postgres.render.com:5432/products_qa
      SPRING_DATASOURCE_USERNAME: breiner
      SPRING_DATASOURCE_PASSWORD: rgiWYoiakZ21ozTKYCvP8q8xY1V0ih3m
      SPRING_JPA_HIBERNATE_DDL_AUTO: update
      SPRING_JPA_PROPERTIES_HIBERNATE_DIALECT: org.hibernate.dialect.PostgreSQLDialect
    networks:
      - products-network
    restart: unless-stopped

networks:
  products-network:
    driver: bridge
```

## CONEXION NEON
```bash
cat > docker-compose.yml << 'EOF'
services:
  springboot-app:
    build: .
    container_name: products-api
    ports:
      - "8080:8080"
    environment:
      SPRING_DATASOURCE_URL: jdbc:
      SPRING_DATASOURCE_USERNAME: 
      SPRING_DATASOURCE_PASSWORD: 
    depends_on:
      postgres:
        condition: service_healthy
    networks:
      - products-network
    restart: unless-stopped

  postgres:
    image: postgres:16
    container_name: postgres-db
    environment:
      POSTGRES_DB: productsqa
      POSTGRES_USER: neondb_owner
      POSTGRES_PASSWORD: npg_wUaAc6TeV1oz
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U neondb_owner"]
      interval: 10s
      timeout: 5s
      retries: 5
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - products-network

volumes:
  postgres_data:

networks:
  products-network:
    driver: bridge
EOF
```

### 1.8 Configurar el Firewall en Azure

En el Portal de Azure:
1. Ve a tu VM1 → **Networking** → **Network Security Group**
2. Agrega reglas de entrada:
   - **Puerto 8080**: Para la API Spring Boot
   - **Puerto 5432**: Solo si necesitas acceso directo a PostgreSQL (opcional)

O desde la terminal:
Si la les aparece el aviso que no se encuentran los comandos, no se preocupen, ese error solo aparece porque la CLI de Azure (az) no está instalada dentro de la máquina, pero no afecta en nada al funcionamiento de tu aplicación, contenedores o Docker Compose.

```bash
# Obtener el NSG de la VM
NSG_NAME=$(az network nsg list --query "[0].name" -o tsv)
RESOURCE_GROUP="tu-resource-group"

# Abrir puerto 8080
az network nsg rule create \
  --resource-group $RESOURCE_GROUP \
  --nsg-name $NSG_NAME \
  --name AllowSpringBoot \
  --priority 1000 \
  --destination-port-ranges 8080 \
  --access Allow \
  --protocol Tcp
```

### 1.9 Iniciar los Contenedores

```bash
# Construir e iniciar los servicios
docker compose up -d --build

# Ver los logs
docker compose logs -f

# Verificar que los contenedores estén corriendo
docker compose ps
```

## Logs del contenedor 
<img width="792" height="727" alt="image" src="https://github.com/user-attachments/assets/1e03452c-591d-4ff9-9487-b4ad681db83c" />

## Arranque de la aplicacion springboot
<img width="793" height="805" alt="image" src="https://github.com/user-attachments/assets/14ca1934-a7f5-444b-9fc4-2343c1fbfb43" />

## Creacion de la tabla 
<img width="773" height="821" alt="image" src="https://github.com/user-attachments/assets/86e17e12-3f9f-4084-a79a-7669eaa46b1c" />


## COMADOS SEGUN LA VERSION DE DOCKER

| Acción                | Versión clásica                | Versión nueva                  |
| --------------------- | ------------------------------ | ------------------------------ |
| Levantar contenedores | `docker-compose up -d`         | `docker compose up -d`         |
| Reconstruir imagen    | `docker-compose up -d --build` | `docker compose up -d --build` |
| Ver logs              | `docker-compose logs -f`       | `docker compose logs -f`       |
| Ver servicios activos | `docker-compose ps`            | `docker compose ps`            |



### 1.10 Probar la API desde el Servidor

```bash
# Obtener la IP pública de la VM1
VM1_IP=$(curl -s ifconfig.me)
echo "IP Pública VM1: $VM1_IP"

# Probar la API localmente
curl http://localhost:8080/api/products

# Crear un producto de prueba
curl -X POST http://localhost:8080/api/products \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Laptop Dell",
    "description": "Laptop Dell Inspiron 15",
    "price": 799.99,
    "stock": 10
  }'
```
<img width="1600" height="178" alt="image" src="https://github.com/user-attachments/assets/8bbdc802-69e1-4e5f-9098-a4f1d40fb6b5" />

---

##  PARTE 2: Configuración de VM2 (Cliente)

### 2.1 Preparar VM2

```bash
# Actualizar sistema
sudo apt update && sudo apt upgrade -y

# Instalar herramientas necesarias
sudo apt install -y curl jq
```

### 2.2 Crear Cliente con Script Bash

```bash
cat > product-client.sh << 'EOF'
#!/bin/bash

# Configuración:  PONGA LA IP PRIVADA  DONDE DICE IP_VM1
API_URL="http://IP_VM1:8080/api/products"

# Colores para la salida
GREEN='\033[0;32m'
RED='\033[0;31m'
BLUE='\033[0;34m'
NC='\033[0m' # No Color

# Función para mostrar el menú
show_menu() {
    clear
    echo -e "${BLUE}================================${NC}"
    echo -e "${BLUE}   CRUD DE PRODUCTOS - CLIENTE${NC}"
    echo -e "${BLUE}================================${NC}"
    echo ""
    echo "1. Listar todos los productos"
    echo "2. Buscar producto por ID"
    echo "3. Crear nuevo producto"
    echo "4. Actualizar producto"
    echo "5. Eliminar producto"
    echo "6. Buscar productos por nombre"
    echo "0. Salir"
    echo ""
    read -p "Seleccione una opción: " option
}

# Listar todos los productos
list_products() {
    echo -e "\n${BLUE}=== LISTA DE PRODUCTOS ===${NC}"
    response=$(curl -s $API_URL)
    echo $response | jq '.'
    read -p "Presione Enter para continuar..."
}

# Buscar producto por ID
get_product() {
    read -p "Ingrese el ID del producto: " id
    echo -e "\n${BLUE}=== PRODUCTO ${id} ===${NC}"
    response=$(curl -s $API_URL/$id)
    echo $response | jq '.'
    read -p "Presione Enter para continuar..."
}

# Crear producto
create_product() {
    echo -e "\n${BLUE}=== CREAR NUEVO PRODUCTO ===${NC}"
    read -p "Nombre: " name
    read -p "Descripción: " description
    read -p "Precio: " price
    read -p "Stock: " stock
    
    response=$(curl -s -X POST $API_URL \
        -H "Content-Type: application/json" \
        -d "{
            \"name\": \"$name\",
            \"description\": \"$description\",
            \"price\": $price,
            \"stock\": $stock
        }")
    
    echo -e "\n${GREEN}Producto creado:${NC}"
    echo $response | jq '.'
    read -p "Presione Enter para continuar..."
}

# Actualizar producto
update_product() {
    read -p "Ingrese el ID del producto a actualizar: " id
    read -p "Nuevo nombre: " name
    read -p "Nueva descripción: " description
    read -p "Nuevo precio: " price
    read -p "Nuevo stock: " stock
    
    response=$(curl -s -X PUT $API_URL/$id \
        -H "Content-Type: application/json" \
        -d "{
            \"name\": \"$name\",
            \"description\": \"$description\",
            \"price\": $price,
            \"stock\": $stock
        }")
    
    echo -e "\n${GREEN}Producto actualizado:${NC}"
    echo $response | jq '.'
    read -p "Presione Enter para continuar..."
}

# Eliminar producto
delete_product() {
    read -p "Ingrese el ID del producto a eliminar: " id
    read -p "¿Está seguro? (s/n): " confirm
    
    if [ "$confirm" = "s" ]; then
        curl -s -X DELETE $API_URL/$id
        echo -e "\n${GREEN}Producto eliminado exitosamente${NC}"
    else
        echo -e "\n${RED}Operación cancelada${NC}"
    fi
    read -p "Presione Enter para continuar..."
}

# Buscar por nombre
search_products() {
    read -p "Ingrese el nombre a buscar: " name
    echo -e "\n${BLUE}=== RESULTADOS DE BÚSQUEDA ===${NC}"
    response=$(curl -s "$API_URL/search?name=$name")
    echo $response | jq '.'
    read -p "Presione Enter para continuar..."
}

# Bucle principal
while true; do
    show_menu
    case $option in
        1) list_products ;;
        2) get_product ;;
        3) create_product ;;
        4) update_product ;;
        5) delete_product ;;
        6) search_products ;;
        0) echo -e "${GREEN}¡Hasta luego!${NC}"; exit 0 ;;
        *) echo -e "${RED}Opción inválida${NC}"; sleep 2 ;;
    esac
done
EOF

# Hacer el script ejecutable
chmod +x product-client.sh
```

<img width="763" height="830" alt="image" src="https://github.com/user-attachments/assets/407de6fc-83fd-4e29-9499-f64ac3993ff6" />



### 2.3 Configurar la IP del Servidor


# Debes usar la **IP PRIVADA** de la VM1 (Servidor)
- y NO la IP pública, ya que ambas máquinas (VM1 y VM2) están en la misma red virtual de Azure.

- Para conocer la IP privada de la VM1, ejecute este comando dentro de la VM1:
```bash
hostname -I
```

- copie la primera IP que aparezca (ejemplo: 10.0.0.4)
- y reemplacela en el siguiente comando:

```bash
read -p "Ingrese la IP PRIVADA de la VM1 (Servidor): " VM1_IP
sed -i "s/IP_VM1/$VM1_IP/g" product-client.sh
```

# Para conocer la IP privada de la VM1, ejecute este comando dentro de la VM1:
```bash
hostname -I
```
<img width="358" height="33" alt="image" src="https://github.com/user-attachments/assets/f067b99b-f21f-4a1d-a606-0e57c5e8b985" />



### 2.4 Ejecutar el Cliente

```bash
./product-client.sh
```

<img width="407" height="516" alt="image" src="https://github.com/user-attachments/assets/865719e3-2ff7-46cc-8de4-679c71a0b1f0" />


---

##  PARTE 3: Pruebas y Verificación

### Pruebas desde VM2 con cURL

```bash
# Reemplaza VM1_IP con la IP real
VM1_IP="tu_ip_vm1"

# GET - Listar productos
curl http://$VM1_IP:8080/api/products

# POST - Crear producto
curl -X POST http://$VM1_IP:8080/api/products \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Mouse Logitech",
    "description": "Mouse inalámbrico",
    "price": 29.99,
    "stock": 50
  }'

# GET - Obtener producto por ID
curl http://$VM1_IP:8080/api/products/1

# PUT - Actualizar producto
curl -X PUT http://$VM1_IP:8080/api/products/1 \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Mouse Logitech MX",
    "description": "Mouse inalámbrico premium",
    "price": 49.99,
    "stock": 30
  }'

# DELETE - Eliminar producto
curl -X DELETE http://$VM1_IP:8080/api/products/1

# GET - Buscar por nombre
curl "http://$VM1_IP:8080/api/products/search?name=mouse"
```

---

##  Comandos Útiles para Administración

### En VM1 (Servidor)

```bash
# Ver logs de la aplicación
docker compose logs -f springboot-app

# Ver logs de PostgreSQL
docker compose logs -f postgres

# Reiniciar servicios
docker compose restart

# Detener servicios
docker compose down

# Detener y eliminar volúmenes (¡cuidado! elimina datos)
docker compose down -v

# Reconstruir la aplicación
docker compose up -d --build

# Conectarse a PostgreSQL
docker exec -it products-postgres psql -U admin -d productsdb

# Ver tablas en PostgreSQL
docker exec -it products-postgres psql -U admin -d productsdb -c "\dt"

# Consultar productos
docker exec -it products-postgres psql -U admin -d productsdb -c "SELECT * FROM products;"
```

---

##  Verificación de Conectividad

### Desde VM2 probar conectividad:

```bash
# Ping a VM1 USANDO LA IP PRIVADA
ping -c 4 <IP_VM1>

# Verificar puerto 8080
nc -zv <IP_VM1> 8080

# O con telnet
telnet <IP_VM1> 8080
```

---

##  Seguridad Adicional (Opcional)

Si quieres mayor seguridad, configura el NSG para que solo VM2 pueda acceder a VM1:

```bash
# Obtener IP de VM2
VM2_IP=$(curl -s ifconfig.me)

# Modificar regla en Azure para permitir solo VM2
az network nsg rule update \
  --resource-group $RESOURCE_GROUP \
  --nsg-name $NSG_NAME \
  --name AllowSpringBoot \
  --source-address-prefixes $VM2_IP
```

---

##  Notas Finales
**El servidor (VM1)** ejecuta Spring Boot y PostgreSQL en contenedores Docker
**El cliente (VM2)** puede ser un script bash, aplicación web, o cualquier cliente HTTP
**La comunicación** se realiza mediante API REST sobre HTTP
**Los datos** persisten en volúmenes Docker incluso si reinicias los contenedores

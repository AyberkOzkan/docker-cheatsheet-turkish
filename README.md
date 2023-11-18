## Docker Cheatsheet

### Basic Docker Commands

- **Mevcut Docker Komutlarını Kontrol Et:** `docker`
- **Docker Sürümünü Göster:** `docker version`
- **Sistem Bilgilerini Göster:** `docker info`
- **Konteyner Çalıştır:** `docker run <image:tag>`
- **Konteyner Oluştur:** `docker create <image:tag>`
- **Konteyner Duraklat:** `docker pause <container_id|container_name>`
- **Duraklatılmış Konteyner'ı Devam Ettir:** `docker unpause <container_id|container_name>`
- **Konteyner'ı Durdur:** `docker stop <container_id|container_name>`
- **Konteyner'ı Başlat:** `docker start <container_id|container_name>`
- **Konteyner'ı Yeniden Başlat:** `docker restart <container_id|container_name>`
- **Konteyner'a Bağlan:** `docker attach <container_id|container_name>`
- **Konteyner'ların Durdurulmasını Bekle:** `docker wait <container_id|container_name>`
- **Konteyner'ı Kaldır:** `docker rm <container_id|container_name>`
- **Konteyner'ları Durdur ve Kaldır:** `docker kill $(docker ps -aq)`

### Docker Image Commands

- **Dockerfile ile Image Oluştur:** `docker build -t <image:tag> .`
- **Docker Hub'dan Image Çek:** `docker pull <image:tag>`
- **Registery'den Image Çek:** `docker pull <registry/image:tag>`
- **Image'ları Listele:** `docker images`
- **Registery'e Image Gönder:** `docker push <repository/image:tag>`
- **Image Dosyasına Etiket Ekle:** `docker tag <source_image:tag> <target_image:tag>`
- **Image Geçmişini Görüntüle (Layers):** `docker history <image:tag>`
- **Image Detaylarını İncele:** `docker inspect <image:tag>`
- **Image Dosyasını Tar Olarak Kaydet:** `docker save <image:tag> -o <filename.tar>`
- **Tar Dosyasından Image Oluştur:** `docker import <filename.tar>`
- **Tar Dosyasından Image Yükle:** `docker load -i <filename.tar>`
- **Image'ları Kaldır:** `docker rmi <image:tag>`

### Docker Container Commands

- **Konteyner'ı Başlat:** `docker start <container_id|container_name>`
- **Konteyner'ı Durdur:** `docker stop <container_id|container_name>`
- **Konteyner'ı Duraklat:** `docker pause <container_id|container_name>`
- **Duraklatılmış Konteyner'ı Devam Ettir:** `docker unpause <container_id|container_name>`
- **Konteyner Çalıştır:** `docker run <image:tag>`
- **Çalışan Konteyner'ları Listele:** `docker ps` | `docker container ls`
- **Konteyner'ları Listele:** `docker ps -a` | `docker container ls -a`
- **Konteyner İçerisinde Komut Çalıştır:** `docker exec -it <container_id|container_name> <command>`
- **Konteyner Loglarını Görüntüle:** `docker logs <container_id|container_name>`
- **Konteyner'ı Yeniden İsimlendir:** `docker rename <old_name> <new_name>`
- **Konteyner'ı Kaldır:** `docker rm <container_id|container_name>`
- **Konteyner Detaylarını İncele:** `docker inspect <container_id|container_name>`
- **Çalışan Bir Konteyner'a Bağlan:** `docker attach <container_id|container_name>`

### Docker Compose Commands

- **Compose Servislerini Oluştur:** `docker-compose build`
- **Compose Servislerini Çalıştır:** `docker-compose up`
- **Compose Servislerini Durdur:** `docker-compose down`
- **Compose Servislerini Başlat:** `docker-compose start`
- **Compose Servislerini Listele:** `docker-compose ls`
- **Compose Servislerini Tek Seferlik Çalıştır:** `docker-compose run <service_name>`
- **Compose Servislerini Kaldır:** `docker-compose rm`
- **Compose Hizmet Durumunu Kontrol Et:** `docker-compose ps`
- **Compose Versiyonunu Görüntülemek:** `docker-compose version`

#### **Linux Üzerinde Docker Composer Kurulumu:**
```bash
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
```

#### **MacOS Üzerinde Docker Composer Kurulumu:**
```bash
brew install docker-compose

docker-compose --version
```

### Docker Compose Dosyası Oluşturma
```bash
nano docker-compose.yml
```
```yaml
version: "3"  # Docker Compose sürüm numarası

services:  # Hizmetlerin başladığı yer
  web:  # Örnek bir hizmet adı
    image: nginx:latest  # Kullanılacak Docker imajı
    container_name: my_web_container  # Docker Container adı
    command: ["nginx", "-g", "daemon off;"]  # Başlatılacak komut
    ports:
      - "8080:80"  # Port yönlendirmesi (host_port:container_port)
    expose:
      - "3000"  # Container'da açık olan port
    environment:
      - MY_ENV_VARIABLE=my_value  # Hizmete özel environment değişkenleri
      - ANOTHER_VARIABLE=another_value
    volumes:
      - ./html:/usr/share/nginx/html  # Host'tan container'a dosya veya klasör montajı
      - /var/www  # Sadece container içinde bir yol
    networks:
      - my_network  # Kullanılacak ağ adı
    depends_on:
      - database  # Hizmetin başlamadan önce başlaması gereken hizmetler
    restart: always  # Hizmetin her zaman yeniden başlaması
    links:
      - database:db  # Legacy link, önerilmez
    logging:
      driver: "json-file"  # Log sürücüsü
      options:
        max-size: "10m"  # Log dosyasının maksimum boyutu
        max-file: "3"  # Maksimum sayıda log dosyası

  database:
    image: mysql:latest
    container_name: my_mysql_container
    ports:
      - "3306:3306"
    volumes:
      - db_data:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=root_password
      - MYSQL_DATABASE=mydatabase
      - MYSQL_USER=myuser
      - MYSQL_PASSWORD=mypassword
    healthcheck:  # Sağlık kontrolü için ayarlar
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
      
    elasticsearch:
      image: docker.elastic.co/elasticsearch/elasticsearch:7.14.0
      container_name: my_elasticsearch_container
      environment:
        - discovery.type=single-node
      ports:
        - "9200:9200"

  kibana:
    image: docker.elastic.co/kibana/kibana:7.14.0
    container_name: my_kibana_container
    environment:
      ELASTICSEARCH_URL: http://elasticsearch:9200
    ports:
      - "5601:5601"
    depends_on:
      - elasticsearch

networks:  # Docker ağlarını tanımlama
  my_network:
    driver: bridge  # Kullanılacak ağ sürücüsü
    ipam:
      driver: default  # IP adreslerini atama sürücüsü
      config:
        - subnet: "172.18.0.0/16"  # Ağ alt ağını belirleme

volumes:  # Docker volumelerini tanımlama
  db_data:
    driver: local  # Volume sürücüsü
    driver_opts:
      type: "nfs"  # Opsiyonel: Volume tipi (örneğin, NFS)
      o: "addr=192.168.1.1,rw"  # Opsiyonel: Volume seçenekleri

configs:  # Docker configs tanımlama
  my_config:
    file: ./config.txt
```
### Docker Volume Commands

- **Volume Oluştur:** `docker volume create <volume_name>`
- **Volume Detaylarını İncele** `docker volume inspect <volume_name>`
- **Volume'leri Listele:** `docker volume ls`****
- **Volume Kaldır** `docker volume rm <volume_name>`

### Docker Networking Commands

- **Network Oluşturma:** `docker network create <network_name>`
- **Network Detaylarını İncele:** `docker network inspect <network_name>`
- **Network'leri Listele:** `docker network ls`
- **Belirli Subnet ve Gateway ile Network Oluşturma:** `docker network create --driver=bridge --subnet=<subnet> --ip-range=<ip_range> --gateway=<gateway_ip> <network_name>`
- **Konteyner'ı Network'e Bağlamak:** `docker network connect <network_name> <container_id | container_name>`
- **Konteyner'ın Network ile Bağlantısını Kesmek:** `docker network disconnect <network_name> <container_id | container_name>`
- **MacVlan Oluşturmak:** `docker network create --driver=macvlan --subnet=<subnet> --gateway=<gateway> -o parent=<parent_interface> <network_name>`

### Docker Logs and Monitoring Commands

- **Tüm Konteynerları görüntüle:** `docker ps -a` | `docker container ls -a`
- **Konteyner Loglarını Görüntüle:** `docker logs <container_id|container_name>`
- **Çalışan İşlemleri Görüntüle:** `docker top <container_id|container_name>`
- **Konteyner Olaylarını izle:** `docker events`
- **Kaynak Kullanımını izle:** `docker stats <container_id|container_name>`
- **Public Portları Göster:** `docker port <container_id|container_name>`

### Docker Prune Commands

- **Asılı Kaynakları Temizle** `docker system prune`
- **Kullanılmayan Konteyner'ları kaldır:** `docker container prune`
- **Asılı Görüntüleri Kaldır:** `docker image prune`
- **Kullanılmayan Volume'leri Kaldır:** `docker volume prune`
- **Kullanılmayan Network'leri Kaldır:** `docker network prune`

### Docker Hub Commands

- **Image Arama** `docker search <image_name>`
- **Docker'a Giriş Yap:** `docker login`
- **Hub'dan Image Çek** `docker pull <image:tag>`
- **Image'ı Hub'a Gönder:** `docker push <repository/image:tag>`
- **Image'a Etiket Ekle:** `docker tag <source_image:tag> <target_image:tag>`
- **Docker'dan Çıkış Yap:** `docker logout`

### Docker Swarm Commands

- **Swarm Durumunu İncele:** `docker info`
- **Swarm Aktif mi Değil mi Kontrolü:** `docker info | grep -q "Swarm: active" && echo "Swarm is active" || echo "Swarm is not active"`
- **Swarm Servislerini Listele:** `docker service ls`
-  **Servis Detaylarını Görüntüle:** `docker service inspect <service_name>`
-  **Servis Güncelleme:** `docker service update --image <new_image><service_name>`
-  **Servis Kaldırma:** `docker service rm <service_name>`
-  **Certificate Authority (CA) Yenileme** `docker swarm ca --rotate`
-  **Swarm'ı Durdurmak:** `docker swarm leave --force`
-  **Swarm Kilidi Açma:** `docker swarm unlock`
-  **Swarm Kilidi Açma Anahtarı Almak:** `docker swarm unlock-key` 

#### **Node Yönetimi**

- **Swarm Node'larını Listele:** `docker node ls`
-  **Node Detaylarını Görüntüle:** `docker node inspect <node_id>`
- **Node Ekleme:** `docker swarm join-token worker`
  
  `docker swarm join-token worker
`
- **Node Kaldırma:** `docker node rm <node_id>`
- **Node Promete Etme:** `docker node promote <node_id>`

#### **Stack Yönetimi**

- **Stack'leri Listele:** `docker stack ls`
-  **Stack Servislerini listele:** `docker stack ls <stack_name>`
-  **Stack Oluşturma:** `docker stack deploy -c <docker-compose-file> <stack_name>`
-  **Stack Kaldırma:** `docker stack rm <stack_name>`
-  **Stack Güncelle:** `docker stack deploy -c <docker-compose-file> <stack_name>`

### **Swarm Visualizer**

- **Swarm Visualizer Servisini Başlatma:** `docker run -it -d -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock dockersamples/visualizer`

### **Portainer**

- **Portainer Konteyner'ını Başlatma:** `docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer`
- **Portainer Konteyner'ını Durdurma:** `docker stop portainer`
- **Portainer Konteyner'ını Silme:** `docker rm portainer`

## Portainer'a Erişim

Portainer artık [http://localhost:9000](http://localhost:9000) adresinden erişilebilir. İlk ziyaretinizde bir kullanıcı adı ve şifre oluşturmanızı isteyecektir.

## Portainer Konteyner'larını Yönetme

### Yeni Bir Container Oluşturma:

Portainer web arayüzünden "Local" → "Containers" → "Add Container" seçeneğini kullanabilirsiniz.

### Konteyner'i Düzenleme:

Portainer web arayüzünden "Local" → "Containers" → Konteyneri seçin ve "Duplicate/Edit" düğmesini kullanın.

### Konteyner'i Durdurma:

Portainer web arayüzünden "Local" → "Containers" → Konteyneri seçin ve "Stop" düğmesini kullanın.

### Konteyner'i Başlatma:

Portainer web arayüzünden "Local" → "Containers" → Konteyneri seçin ve "Start" düğmesini kullanın.

### Konteyner'i Silme:

Portainer web arayüzünden "Local" → "Containers" → Konteyneri seçin ve "Remove" düğmesini kullanın.

## Portainer Hizmet ve Ağları Yönetme

### Yeni Bir Servis Oluşturma:

Portainer web arayüzünden "Local" → "Stacks" → "Add Stack" seçeneğini kullanabilirsiniz.

### Servisi Düzenleme:

Portainer web arayüzünden "Local" → "Stacks" → Servisi seçin ve "Edit Stack" düğmesini kullanın.

### Servisi Silme:

Portainer web arayüzünden "Local" → "Stacks" → Servisi seçin ve "Remove Stack" düğmesini kullanın.

### Yeni Bir Ağ Oluşturma:

Portainer web arayüzünden "Local" → "Networks" → "Add Network" seçeneğini kullanabilirsiniz.

### Ağı Düzenleme:

Portainer web arayüzünden "Local" → "Networks" → Ağı seçin ve "Edit Network" düğmesini kullanın.

### Ağı Silme:

Portainer web arayüzünden "Local" → "Networks" → Ağı seçin ve "Remove Network" düğmesini kullanın.

### **Secret**

- **Secret Oluşturma:** `docker secret create <secret_name> <file_path>`
- **Tüm Secret'ları Listele:** `docker secret ls`
- **Secret Bilgilerini Görüntüle:** `docker secret inspect <secret_name>`
- **Servise Secret Eklemek:** `docker service create --name myservice --secret <secret_name> myimage`

#### Stack için;

```yaml
version: "3.1"

services:
  myservice:
    image: myimage
    secrets:
      - <secret_name>
secrets:
  <secret_name>:
    file: ./path/to/secret/file
```
- **Secret'i Güncelleme:** `docker secret update --secret <secret_name> --new-file <new_file_path>`
- **Secret Silme:** `docker secret rm <secret_name>`
- 
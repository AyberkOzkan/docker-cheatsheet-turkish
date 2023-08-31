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
- **Compose Servislerini Başlat:** `docker-compose start`
- **Compose Servislerini Listele:** `docker-compose ls`
- **Compose Servislerini Tek Seferlik Çalıştır:** `docker-compose run <service_name>`
- **Compose Servislerini Kaldır:** `docker-compose rm`
- **Compose Hizmet Durumunu Kontrol Et:** `docker-compose ps`

### Docker Volume Commands

- **Volume Oluştur:** `docker volume create <volume_name>`
- **Volume Detaylarını İncele** `docker volume inspect <volume_name>`
- **Volume'leri Listele:** `docker volume ls`****
- **Volume Kaldır** `docker volume rm <volume_name>`

### Docker Networking Commands

- **Network Oluşturma:** `docker network create <network_name>`
- **Network Detaylarını İncele:** `docker network inspect <network_name>`
- **Network'leri Listele:** `docker network ls`

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

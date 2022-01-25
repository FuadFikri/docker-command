# Perintah Docker

## Melihat daftar image
docker image ls

## Download image
docker pull  namaimage:tag

## Hapus image
docker image rm nama_image:tag


## melihat all container
docker container ls -a


## melihat container yang berjalan
docker container ls


## membuat container
docker container create --name nama_container nama_image:tag

## Menjalankan container
docker container start container_id atau container_name

## Menghentikan container
docker container stop container_id atau container_name


## hapus container
docker container rm container_name



## Logs
docker container logs container_id atau container_name
docker container logs -f container_name atau container_id



## Docker exec
- masuk ke container, kita bisa menggunakan program bash script

docker container exec -i it container_id atau container_name /bin/bash
- -i : argumentnya interaktif (menjaga input tetap aktif)
- -t : argument untuk pseudo-TTY(terminal akses)
- /bin/bash contoh kode program didalam container


## Container port
- saat menjalankan container, container tersebut terisolasi didalam docker
- sistem host(misal laptop kita) tidak bisa mengakses aplikasi yang ada didalam container secara langsung. 

## Port Forwarding
 - meneruskan sebuah port yang terdapat di sistem host kedalam docker container
 - cara ini cocok jika kita ingin mengekspos port yang ada di container keluar melalui sistem Host kita
 - untuk menlakukan port forwarding, kita bisa menggunakan perintah berikut saat create container
  docker container create --name nama_container --publish port_host:port_container image:tag
 - jika ingin melakukan port forwarding lebih dari 1, kita bisa tambahkan 2 kali parameter --publish
 - contoh: 
    docker container create --name contohnginx --publish 8080:80 nginx:latest
    - nginx akan bisa diakses pada port 8080 di komputer host
 
 
## Environment variable
 docker container create --name container_name --env KEY="VALUE" --env KEY="VALUE" --env KEY="VALUE" image:tag
 
## Container stats
 docker container stats
 
 
## Container resource limit
- maksimal resource yang bisa digunakan oleh containernya
- menentukan max jumlah cpu  : --cpus
- menentukan max jumlah memory  : --memory
  docker container create --name my-nginx --publish 8081:80 --memory 100m --cpus 0.5 nginx:latest
  
## Bind mount
- kemampuan melakukan mounting (sharing) file atau folder yang terdapat di sistem host ke container yang terdapat di docker
- Fitur ini sangat berguna ketika misal kita ingin mengirim konfigurasi dari luar container, atau misal menyimpan data yang dibuat di aplikasi di dalam container ke dalam folder di sistem host
### Parameter
	- type : tipe mount, bind, atau volume
	- source : lokasi file / folder di sistem host
	- destionation : lokasi file / folder di container
	- readonly:  jika ada, maka file atau folder hanya bisa dibaca di container, tidak bisa ditulis
	
- docker container create --name namacontainer --mount “type=bind,source=folder_host,destination=folder_container,readonly” image:tag

## Docker Volume
- Docker Volume mirip dengan Bind Mounts, bedanya adalah terdapat management Volume, dimana kita bisa membuat Volume, melihat daftar Volume, dan menghapus Volume
- di versi terbaru direkomendasikan menggunakan Docker Volume dari pada bind mount
- Volume  bisa dianggap storage yang digunakan untuk menyimpan data, bedanya dengan Bind Mounts, pada bind mounts, data disimpan pada sistem host, sedangkan pada volume, data di manage oleh Docker

### Melihat volume
- docker volume ls

### Membuat volume
- docker volume create nama_volume


### Hapus VOlume
- docker volume rm nama_volume

### Container Volume
- membuat volume
	- docker volume create mongodata
- menmbuat container menggunakan volume
	- docker container create --name my-mongo --mount "type=volume, source=mongodata, destination=/data/db" --publish 27019:27017 mongo:latest
	

  

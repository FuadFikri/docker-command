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
 
 contoh: 
 docker container create --name contohnginx --publish 8080:80 nginx:latest
 


## Volume

It's a presistent storage, jo tab bhi rehti hey jab hamara container delete ho jata hey. Ap apna custome volume bhi bana saktey ho docker k ander ya phir apni device (host) per majud kisi folder ko bhi container k ander mount kar saktey ho

## Mounting Host Folder inside Container

```bash
$ docker run -v host_dir_path:container_dir_path image_name
```

## Creating Custome Volume

You can also create custome volume inside docker and manage through docker, let see how to create custome volume

```bash
docker volume create custom_data
```

**Mount Volume**

```bash
docker run --volume custom_data:/home/volume image_name
```

Yeah command `/home` directory k ander aik `volume` directory banaye gi or usay link kar dey gi hamarey volume k sath yani volume ka sara data usmey show hoga.

## Where is volume data?

Docker apney volumes ka data store karta hey:-

```bash
/var/lib/docker/volumes
```

Ya phir ap paney sarey volums ko docker k desktop client k GUI mey dehk saktey heyn.

## Remove a volume

```bash
docker volume rm volume_name
```



# Lighterpack for Umbrel

Native Umbrel app for Lighterpack.

## Architecture

This app intentionally does not use Dockge or Docker-in-Docker.

- **Lighterpack:** existing private/local image `ligterpack:111`
- **MongoDB:** official `mongo:5.0` image for AMD64
- **Persistent data:** Umbrel `APP_DATA_DIR`
- **Reverse proxy:** Umbrel `app_proxy`

The Lighterpack image is private and is therefore not included in this repository.

## Preload the Lighterpack image

The existing image must be present in the Umbrel host Docker before installing the app.

If migrating from the previous Dockge/DIND installation, export it from the DIND Docker and load it into the host Docker:

```bash
sudo docker -H unix:///home/umbrel/umbrel/app-data/dockge/data/docker/docker.sock \
  save ligterpack:111 | sudo docker load
```

Verify:

```bash
sudo docker images ligterpack --no-trunc
```

The expected image ID is:

```
sha256:1c190bdb7a08eb163e4446792d98b7afd6cf466fcbe11cafffd61e9ff60d011a
```

## Database migration

Do not copy the old MongoDB WiredTiger files.

Restore the known-good logical dump into the new MongoDB container instead. This avoids carrying forward the previous WiredTiger corruption.

## Persistent directories

The app uses:

- `data/mongodb`
- `data/images`
- `data/uploads`

The old Dockge/DIND Lighterpack installation should remain untouched until the native installation has been fully verified.

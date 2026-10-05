# IggyDev Umbrel Community App Store

Community apps maintained by IggyDev.

## Dockge Host

**Dockge Host** is a standalone Dockge 1.5.0 package designed for Umbrel power users.

Unlike the stock Umbrel Dockge package, it connects directly to the Umbrel host Docker
daemon and mounts the persistent Dockge stacks directory at the **same absolute path**
inside the Dockge container.

This is important for Compose bind mounts. For example:

```
/home/umbrel/umbrel/app-data/dockge/data/dockge-stacks/lighterpack/images
```

is visible at exactly that path to both Dockge and the host Docker daemon.

### Why this exists

The stock Umbrel Dockge package uses Docker-in-Docker. Its nested Docker daemon has a
separate filesystem namespace, so host paths used by Compose bind mounts are not
automatically visible to it.

Dockge Host removes that extra Docker daemon and talks directly to the host Docker
socket.

### Important security warning

This app mounts:

- `/var/run/docker.sock`
- the persistent Dockge stacks directory

That gives Dockge effectively full administrative control over the host Docker daemon.
Only install it on a system you administer and only run Compose files you trust.

The existing Umbrel Dockge app is intentionally **not modified**. Install this app
alongside the stock Dockge while testing and migrating.

## Repository

https://github.com/iggydev/umbrel-community-app-store

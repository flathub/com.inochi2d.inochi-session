# com.inochi2d.inochi-session

## Update Base

```sh
podman run --rm \
    -v$(pwd):/opt:Z --workdir=/opt \
    docker://ghcr.io/flathub/flatpak-external-data-checker:latest \
    --edit-only ./com.inochi2d.inochi-session.yml 
```

## Update dependencies

Get the grillo-delmal/inochi-session-devtest repository.

```sh
cd ..
git clone https://github.com/grillo-delmal/inochi-session-devtest
cd inochi-session-devtest
```

Use the update-dependencies.sh

```sh
./update-dependencies.sh \
    --yml-session=../com.inochi2d.inochi-session/com.inochi2d.inochi-session.yml \ 
    --skip-patch
```

## Local Test

```
flatpak-builder --default-branch=localbuild --force-clean --repo=./repo-dir ./build-dir com.inochi2d.inochi-session.yml

flatpak build-bundle \
    --runtime-repo=https://flathub.org/repo/flathub.flatpakrepo \
    ./repo-dir \
    inochi-session.x86_64.flatpak \
    com.inochi2d.inochi_session localbuild
flatpak build-bundle \
    --runtime \
    ./repo-dir \
    inochi-session.x86_64.debug.flatpak \
    com.inochi2d.inochi_session.Debug localbuild

flatpak --user -y install inochi-session.x86_64.flatpak
flatpak --user -y install inochi-session.x86_64.debug.flatpak
```
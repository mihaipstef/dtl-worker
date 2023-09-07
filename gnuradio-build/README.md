# DTL Gnuradio build image

## Build Alpine packages

1. Build docker image with all tools required to compile and create apk packages.

```
docker build -t gnuradio-build:latest .
```

2. Start a docker container that mounts the `aports` and `repository` folders to the host.


```
docker run --rm -v ~/dtl-flows/dtl-gw/gnuradio-build/aports:/aports -v ~/dtl-flows/packages:/packages -ti gnuradio-build sh
```

3. Build the packages

```
cd /aports/libiio
abuild -r -P /packages
sudo apk add --repository /packages/aports/ libiio
```

Continue with the rest of the packages (in this order): `libad9361`, `volk`, `gnuradio` and `gr-dtl`.
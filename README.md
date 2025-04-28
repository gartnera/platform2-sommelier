# sommelier

This is a copy of the [sommelier](https://chromium.googlesource.com/chromiumos/platform2.git/+/main/vm_tools/sommelier) source code from the [platform2 repo](https://chromium.googlesource.com/chromiumos/platform2.git/).

I use this program to run Xorg applications on wayland with custom scale factors.

## building

```
cd vm_tools/sommelier
meson setup --prefix=/usr ./ build
cd build
meson compile
```

## usage

### individual client

```
sommelier --noop-driver --display=wayland-1 -X --scale=1.25 xterm
```

### shared server

In this mode, you only need to run sommelier once.


```
sommelier --noop-driver --display=wayland-1 -X --x-display=2 --no-exit-with-child --scale=1.25 true
```

```
export DISPLAY=2
xterm
```

## updating source

Get sparse sources:

```
git clone -n --depth=1 --filter=tree:0 \
  https://chromium.googlesource.com/chromiumos/platform2.git
cd platform2
git sparse-checkout set --no-cone /vm_tools/sommelier
git checkout
```

Copy new sources over:

```
cp -r ../platform2/* .
```

Amend existing import commit and force push.
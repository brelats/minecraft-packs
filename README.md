# minecraft-packs

Resource packs for Minecraft plugins, served to players through [jsDelivr](https://www.jsdelivr.com).

Plugins that need a resource pack send players a link to it. Hosting the pack from the Minecraft server
itself means opening an extra port, which many hosts don't allow, so the packs are published here instead
and downloaded from a free, global CDN. Server owners have nothing to set up.

## Layout

Each plugin has its own folder, and each release that changes a plugin's packs is a tag named
`<plugin>-<version>`:

```
<plugin>/
  <pack>.zip
```

A pack is downloaded from:

```
https://cdn.jsdelivr.net/gh/brelats/minecraft-packs@<plugin>-<version>/<plugin>/<pack>.zip
```

Tags are never moved, so a link keeps pointing at the same file forever. Older plugin versions keep using
the packs of their own tag, and the main branch only holds the latest packs of each plugin.

## How the packs are made

A plugin often builds a different pack for each Minecraft version (and for some of its settings). Before
a release, the plugin itself is started on a server of every supported Minecraft version and writes every
pack it can build. Each pack is named after a hash of its contents.

The plugin's jar carries the list of its published packs. On start, it builds its pack as usual, looks up
that hash, and sends players the matching link here. If the pack isn't in the list (for example, when a
server owner customised it), the plugin serves the pack itself instead.

The files are generated: don't edit them by hand.

## Using a pack

If you run one of these plugins, you don't need anything from this repository; the plugin picks the right
pack on its own. To use the pack another way, get it from the plugin's own folder (`plugins/<Plugin>/`)
on your server, which always matches your setup.

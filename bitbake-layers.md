# Usage
```
usage: bitbake-layers [-d] [-q] [-F] [--color COLOR] [-h] <subcommand> ...  
  
BitBake layers utility  
  
optional arguments:  
 -d, --debug           Enable debug output  
 -q, --quiet           Print only errors  
 -F, --force           Force add without recipe parse verification  
 --color COLOR         Colorize output (where COLOR is auto, always, never)  
 -h, --help            show this help message and exit  
  
subcommands:  
 <subcommand>  
   show-layers         show current configured layers.  
   show-overlayed      list overlayed recipes (where the same recipe exists in another layer)  
   show-recipes        list available recipes, showing the layer they are provided by  
   show-appends        list bbappend files and recipe files they apply to  
   show-cross-depends  Show dependencies between recipes that cross layer boundaries.  
   add-layer           Add one or more layers to bblayers.conf.  
   remove-layer        Remove one or more layers from bblayers.conf.  
   flatten             flatten layer configuration into a separate output directory.  
   layerindex-fetch    Fetches a layer from a layer index along with its dependent layers, and adds them to conf/bblayers.conf.  
   layerindex-show-depends  
                       Find layer dependencies from layer index.  
   create-layer        Create a basic layer  
  
Use bitbake-layers <subcommand> --help to get help on a specific command
```

Layers need to be `create`d before being `add`ed.
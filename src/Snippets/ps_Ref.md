# PS Reference

### ps

The `ps` command is generally an underutilized asset when getting information quickly.

A useful alias to start with is:

`sudo ps awxf -eo pid,user,%cpu,%mem,args`

-   `w` - wideoutput.
-   `x` - include processes that don't have a controlling terminal (background jobs.)
-   `f` - shows process heirarchy.
-   `a` - include processes belonging to other users.

-   `e` - every process.
-   `o` - specify output fields.

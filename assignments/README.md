## Known bugs

- Throughout the codebase, I have used register R5 carelessly with resource manager. Although everything works till stage 27, any call to resource manager does rewrite R5. It can be fixed by changing terminal_read and terminal_write as they are the only dependents of R5.

- Thanks to [Alen](https://github.com/Anonymous-AAA) for finding this out, any user space physical address which are used throughout interrupts, can point to the wrong memory page if it gets swapped while the process is blocked. Most notably in buffered_read, termina_read, and any other return address calculation depending on the implementation. I have noticed some return addresses calculation points, mainly in int_4, int_5, int_6, int_7 which can potentially break the system. However I tried fixing it and stage 27 broke again so Im gonna leave that alone for now <3.

- Resource manager must be carefully dealt with for acquiring/releasing inodes as I switched R2 and R3 parameters.

## Stage 28 Bugs 

- There was a build error for the expl compiler
- The expl compiler provided in the tarball of nexsm doesnt support colons. (Maybe its an older build)
- For peterson algorithm, the uallocated space after access_lock_table is used. The splconstants.cfg file was edited to avail the new constants in mod_8.spl
- Stage 27 Assignment 5, merging program goes to a rare deadlock in 28. I still have not found out the bug / fix. 
- Stage 27 Assignment 4, has some synchronization problems in the expl code. It magically works in stage 27 but not completely in 28.

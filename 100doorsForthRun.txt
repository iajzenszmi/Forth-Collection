ian@ian-HP-Convertible-x360-11-ab1XX:~$ gforth 100doors.forth
1 4 9 16 25 36 49 64 81 100 
Gforth 0.7.3, Copyright (C) 1995-2008 Free Software Foundation, Inc.
Gforth comes with ABSOLUTELY NO WARRANTY; for details type `license'
Type `bye' to exit
bye 
ian@ian-HP-Convertible-x360-11-ab1XX:~$ cat 100doors.forth
: toggle ( c-addr -- )  \ toggle the byte at c-addr
    dup c@ 1 xor swap c! ;

100  1+ ( 1-based indexing ) constant ndoors
create doors  ndoors allot

: init ( -- )  doors ndoors erase ;  \ close all doors

: pass ( n -- )  \ toggle every nth door
    ndoors over do
        doors i + toggle
    dup ( n ) +loop drop ;

: run ( -- )  ndoors 1 do  i pass  loop ;
: display ( -- )  \ display open doors
    ndoors 1 do  doors i + c@ if  i .  then loop cr ;

init run display
ian@ian-HP-Convertible-x360-11-ab1XX:~$ 

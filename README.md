# utl-using-sql-arrays-and-do_over-to-cast_0_1-to-Y-N
Using sql arrays and do_over to cast (0,1) to (Y,N)
    Using sql arrays and do_over to cast (0,1) to (Y,N)

    Using sql arrays for redefine 26 variables;

    Github
    https://tinyurl.com/488u32tm
    https://github.com/rogerjdeangelis/utl-using-sql-arrays-and-do_over-to-cast_0_1-to-Y-N

    Related GitHub Repos
    https://tinyurl.com/cx4c2ymp
    https://github.com/rogerjdeangelis?tab=repositories&q=sql+array%27&type=&language=&sort=

    I need to convert (0,1) to ('Y','N') for 26 numeric variables keeping the same names using SQL.
    Do not be afraid of repetitive code, a good complier can result in
    code that is faster than looping.

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    data have;
        do _=1 to 2;
          if _=1 then do;
             A=0; G=0; L=0; Q=0; V=0;
             B=0; H=0; M=0; R=0; W=0;
             C=0; I=0; N=0; S=0; X=0;
             D=0; J=0; O=0; T=0; Y=0;
             E=0; K=0; P=0; U=0; Z=0;
          end;
          else do;
             A=1; G=1; L=1; Q=1; V=1;
             B=1; H=1; M=1; R=1; W=1;
             C=1; I=1; N=1; S=1; X=1;
             D=1; J=1; O=1; T=1; Y=1;
             E=1; K=1; P=1; U=1; Z=1;
          end;
          output;
        end;
    stop;
    run;quit;

    WORK.HAVE total obs=2

     _ A G L Q V B H M R W C I N S X D J O T Y E K P U Z

     1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
     2 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    * this is set in my autoexwc;
    %let letters=A B C D E F G H I J K L M N O P Q R S T U V W X Y Z;

    %array(_ltr,values=&letters);

    *just in case you are testing;
    proc datasets nodetails nolist;
      delete want;
    run;quit;

    proc sql;
      create
        table want as
      select
        _
       ,%do_over(_ltr,phrase=%str(
          ifc(_=1,'Y','N','N') as ?),between=comma)
      from
         have
    ;quit;

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

     WORK.WANT total obs=2

     _ A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

     1 Y Y Y Y Y Y Y Y Y Y Y Y Y Y Y Y Y Y Y Y Y Y Y Y Y Y
     2 N N N N N N N N N N N N N N N N N N N N N N N N N N

    /*                                _
      __ _  ___ _ __     ___ ___   __| | ___
     / _` |/ _ \ `_ \   / __/ _ \ / _` |/ _ \
    | (_| |  __/ | | | | (_| (_) | (_| |  __/
     \__, |\___|_| |_|  \___\___/ \__,_|\___|
     |___/
    */

    data gencde;

       %do_over(_ltr,phrase=%str(put ",ifc(_=1,'Y','N','N') as ?";) );

    run;quit;

    ,ifc(_=1,'Y','N','N') as A
    ,ifc(_=1,'Y','N','N') as B
    ,ifc(_=1,'Y','N','N') as C
    ,ifc(_=1,'Y','N','N') as D
    ,ifc(_=1,'Y','N','N') as E
    ,ifc(_=1,'Y','N','N') as F
    ,ifc(_=1,'Y','N','N') as G
    ,ifc(_=1,'Y','N','N') as H
    ,ifc(_=1,'Y','N','N') as I
    ,ifc(_=1,'Y','N','N') as J
    ,ifc(_=1,'Y','N','N') as K
    ,ifc(_=1,'Y','N','N') as L
    ,ifc(_=1,'Y','N','N') as M
    ,ifc(_=1,'Y','N','N') as N
    ,ifc(_=1,'Y','N','N') as O
    ,ifc(_=1,'Y','N','N') as P
    ,ifc(_=1,'Y','N','N') as Q
    ,ifc(_=1,'Y','N','N') as R
    ,ifc(_=1,'Y','N','N') as S
    ,ifc(_=1,'Y','N','N') as T
    ,ifc(_=1,'Y','N','N') as U
    ,ifc(_=1,'Y','N','N') as V
    ,ifc(_=1,'Y','N','N') as W
    ,ifc(_=1,'Y','N','N') as X
    ,ifc(_=1,'Y','N','N') as Y
    ,ifc(_=1,'Y','N','N') as Z

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

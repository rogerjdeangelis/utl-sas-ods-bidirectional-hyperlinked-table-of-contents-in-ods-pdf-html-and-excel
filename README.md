# utl-sas-ods-bidirectional-hyperlinked-table-of-contents-in-ods-pdf-html-and-excel
sas ods bidirectional hyperlinked table of contents in ods pdf htmp and excel   
    %let pgm=utl-sas-ods-bidirectional-hyperlinked-table-of-contents-in-ods-pdf-html-and-excel;

    sas ods bidirectional hyperlinked table of contents in ods pdf htmp and excel

    These solutions have both hyperlinks to sheets and hyperlinks bak to the table of contents.
    In addition unwanted levels in the table of contebta are removed.

            1 sas ods excel hyperlinked table of contents
            2 sas ods pdf hyperlinked table of contents
            3 sas ods htmp hyperlinked table of contents

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************************/
    /*                                   |                                                |                                               */
    /* 1 SAS ODS EXCEL WORKBOOK          |                                                |                                               */
    /* ========================          |                                                |                                               */
    /*                                   |                                                |                                               */
    /*              INPUT                |         PROCESS                                |             OUTPUT                            */
    /*                                   |                                                |                                               */
    /*                                   |  title;                                        |                                               */
    /* sashelp,class(where=(sex="F"))    |  footnote;                                     |    +----------------------------+             */
    /* sashelp,class(where=(sex="M"))    |                                                |    |                  A         |             */
    /*                                   |  %utlfkil(d:/xls/cynthia.xlsx);                |    |------------------+---------|             */
    /*                                   |                                                |  1 |Detail Report of Males      |             */
    /*                                   |  ods excel file="d:/xls/cynthia.xlsx"          |    |----------------------------+             */
    /*                                   |     style=statistical;                         |  2 |  Demographics (HYPERLINK)  |             */
    /*                                   |                                                |    +------------------+---------+             */
    /*                                   |  ods excel options(                            |  3 |Detail Report of Females    |             */
    /*                                   |        embedded_titles    = "yes"              |    |----------------------------+             */
    /*                                   |        contents           = "yes"              |  4 |  Demographics (HYPERLINK)  |             */
    /*                                   |        embedded_footnotes = "yes");            |    +------------------+---------+             */
    /*                                   |                                                |                                               */
    /*                                   |  footnote                                      |  [Table of Contehts]                          */
    /*                                   |    link="#'The Table of Contents'!a1"          |                                               */
    /*                                   |         "Return to TOC";                       |    ----------------------------------+        */
    /*                                   |  run;quit;                                     |    |     A   |  B  |  C    |    D    |        */
    /*                                   |                                                |    ----------------------------------+        */
    /*                                   |  ods excel options(sheet_name="MALES");        |  1 |NAME     | SEX |HEIGHT |  WEIGHT |        */
    /*                                   |  ods proclabel= "Detail Report of Males";      |    +---------+-----+-------+---------+        */
    /*                                   |                                                |  2 | ALFRED  |  M  |  69   |  112.5  |        */
    /*                                   |  title "Male Students";                        |    +---------+-----+-------+---------+        */
    /*                                   |  proc print data=sashelp.class                 |     ...                                       */
    /*                                   |    (where=(sex="M"))                           |    +---------+-----+-------+---------+        */
    /*                                   |    contents="Demographics";                    |  N | WILLIAM |  M  | 66.5  |  112    |        */
    /*                                   |  run;                                          |    +---------+-----+-------+---------+        */
    /*                                   |                                                |                                               */
    /*                                   |  ods excel options(sheet_name="FEMALES");      |    Return to TOC (hyperlink)                  */
    /*                                   |  ods proclabel= "Detail Report of Females";    |                                               */
    /*                                   |                                                |  [MALES]                                      */
    /*                                   |  title "Female Students";                      |                                               */
    /*                                   |  proc print data=sashelp.class                 |    ---------------------------------+         */
    /*                                   |    (where=(sex="F"))                           |    |     A   |  B  |  C    |   D    |         */
    /*                                   |    contents="Demographics";                    |    ---------------------------------+         */
    /*                                   |  run;quit;                                     |  1 | NAME    | SEX |HEIGHT | WEIGHT |         */
    /*                                   |                                                |    +---------+-----+-------+--------+         */
    /*                                   |  ods excel close;                              |  2 | ALICE   |  F  |  69   | 112.5  |         */
    /*                                   |                                                |    +---------+-----+-------+--------+         */
    /*                                   |                                                |                                               */
    /*                                   |                                                |    +---------+-----+-------+--------+         */
    /*                                   |                                                |  N | BARBARA |  F  | 66.5  | 112    |         */
    /*                                   |                                                |    +---------+-----+-------+--------+         */
    /*                                   |                                                |                                               */
    /*                                   |                                                |    Return to TOC (hyperlink)                  */
    /*                                   |                                                |                                               */
    /*                                   |                                                |  [FEMALES]                                    */
    /*                                   |                                                |                                               */
    /*-----------------------------------|------------------------------------------------|-----------------------------------------------*/ -
    /*                                   |                                                |                                               */
    /* 2 SAS ODS PDF DOCUMENT            |                                                |                                               */
    /* ======================            |                                                |                                               */
    /*                                   |                                                |                                               */
    /*    data have;                     |  %utlfkil(d:/pdf/want.pdf);                    |  ------- Table of Contents -------            */
    /*      retain count 1;              |                                                |                                               */
    /*      set class ;                  |  title;                                        |  Table of Contents                            */
    /*    run;quit;                      |  footnote;                                     |  Male Participants   .  .  .  .  . 1          */
    /*                                   |                                                |  Demographics        .  .  .  .  . 1          */
    /* COUNT NAME SEX AGE HEIGHT WEIGHT  |  ods escapechar="^";                           |  Female Participants .  .  .  .  . 2          */
    /*                                   |                                                |  Demographics        .  .  .  .  . 2          */
    /* 1  Alfred   M   14  69.0   112.5  |  ods pdf file="d:/pdf/want.pdf" contents ;     |                                               */
    /* 1  Alice    F   13  56.5    84.0  |                                                |  Male Students                                */
    /* 1  Barbara  F   13  65.3    98.0  |  ods proclabel="Male Participants";            |                                               */
    /* 1  Carol    F   14  62.8   102.5  |  title "Male Students";                        |  NAME            AGE     HEIGHT     WEIGHT    */
    /* 1  Henry    M   14  63.5   102.5  |   proc report nowd data=have                   |                                               */
    /*                                   |      (where=(sex="M")) contents="Demographics";|  Alfred           14         69      112.5    */
    /*                                   |      col count name age height weight;         |  Henry            14       63.5      102.5    */
    /*                                   |      define count / group noprint;             |  James            12       57.3         83    */
    /*                                   |       break before count / contents="" page;   |  Jeffrey          13       62.5         84    */
    /*                                   |      compute after;                            |  John             12         59       99.5    */
    /*                                   |       lyn = "^S={URL='anchor.pdf#PAGE=1'       |  Philip           16         72        150    */
    /*                                   |           color=blue                           |  Robert           12       64.8        128    */
    /*                                   |           just=left}Return to TOC" ;           |                                               */
    /*                                   |       line lyn $64.;                           |  Return to TOC                                */
    /*                                   |      endcomp;                                  |                                               */
    /*                                   |   run;                                         |  Male Students                                */
    /*                                   |                                                |                                               */
    /*                                   |  ods proclabel="Female Participants";          |  NAME            AGE     HEIGHT     WEIGHT    */
    /*                                   |  title "Female Students";                      |  Alice            13       56.5         84    */
    /*                                   |   proc report nowd data=have                   |  Barbara          13       65.3         98    */
    /*                                   |      (where=(sex="F")) contents="Demographics";|  Carol            14       62.8      102.5    */
    /*                                   |      col count name age height weight;         |  Jane             12       59.8       84.5    */
    /*                                   |      define count / group noprint;             |  Janet            15       62.5      112.5    */
    /*                                   |       break before count / contents="" page;   |  Joyce            11       51.3       50.5    */
    /*                                   |      compute after;                            |                                               */
    /*                                   |       lyn = "^S={URL='anchor.pdf#PAGE=1'       |  Return to TOC                                */
    /*                                   |           color=blue                           |                                               */
    /*                                   |        just=left }Return to TOC" ;             |                                               */
    /*                                   |    line lyn $64.;                              |                                               */
    /*                                   |   endcomp;                                     |                                               */
    /*                                   |  run;quit;                                     |                                               */
    /*                                   |  ods pdf close;                                |                                               */
    /*                                   |                                                |                                               */
    /*------------------------------------------------------------------------------------------------------------------------------------*/
    /*                                   |                                                           |                                    */
    /* 2 SAS ODS PDF DOCUMENT            | title;                                                    | ---- Table od Contents ----        */
    /* ======================            | foornote;                                                 |                                    */
    /*                                   |                                                           | List of Female Students            */
    /*    data have;                     | %utlfkil(d:/pages/toc.html);                              | List of Female Students            */
    /*      retain count 1;              | %utlfkil(d:/pages/males.html);                            |                                    */
    /*      set class ;                  | %utlfkil(d:/pages/feales.htm);                            |                                    */
    /*    run;quit;                      |                                                           |  MALE STUDENTS                     */
    /*                                   | title "---- Table of Contents ----";                      |                                    */
    /* COUNT NAME SEX AGE HEIGHT WEIGHT  | ods escapechar="^";                                       |  +-------------------------------+ */
    /*                                   | ods html body="toc.html" path="d:/pages";                 |  |NAME     | SEX |HEIGHT | WEIGHT| */
    /* 1  Alfred   M   14  69.0   112.5  | ods text="<a href='d:/pages/females.html'>                |  +---------+-----+-------+-------+ */
    /* 1  Alice    F   13  56.5    84.0  |  List of Female Students</a>";                            |  | ALFRED  |  M  |  69   | 112.5 | */
    /* 1  Barbara  F   13  65.3    98.0  | ods text="<a href='d:/pages/males.html'>                  |  +---------+-----+-------+-------+ */
    /* 1  Carol    F   14  62.8   102.5  |  List of Male Students</a>";                              |   ...                              */
    /* 1  Henry    M   14  63.5   102.5  | ods html close;                                           |  +---------+-----+-------+-------+ */
    /*                                   |                                                           |  | WILLIAM |  M  | 66.5  | 112   | */
    /*                                   | ods html body="males.html" path="d:/pages";               |  +---------+-----+-------+-------+ */
    /*                                   | title "Male Students";                                    |  | Return to Tabke of Contents   | */
    /*                                   | proc report data=sashelp.class(where=(sex="M"));          |  +---------+-----+-------+-------+ */
    /*                                   |  compute after;                                           |                                    */
    /*                                   |   lyn =                                                   |                                    */
    /*                                   |   "^{style [URL='d:/pages/toc.html']Table of Contents}";  |                                    */
    /*                                   |   line lyn $64.;                                          |  FEMALE STUDENTS                   */
    /*                                   |  endcomp;                                                 |                                    */
    /*                                   | run;quit;                                                 |  +-------------------------------+ */
    /*                                   |                                                           |  | NAME    | SEX |HEIGHT | WEIGHT| */
    /*                                   | ods html body="females.html" path="d:/pages";             |  +---------+-----+-------+-------+ */
    /*                                   | title "Female Students";                                  |  | ALICE   |  F  |  69   | 112.5 | */
    /*                                   | proc report data=sashelp.class(where=(sex="F"));          |  +---------+-----+-------+-------+ */
    /*                                   |  compute after;                                           |                                    */
    /*                                   |   lyn =                                                   |  +---------+-----+-------+-------+ */
    /*                                    |    "^{style [URL='d:/pages/toc.html']Table of Contents}"; |  | BARBARA |  F  | 66.5  | 112   | */
    /*                                   |   line lyn $64.;                                          |  +---------+-----+-------+-------+ */
    /*                                   |  endcomp;                                                 |  | Return to Tabke of Contents   | */
    /*                                   | run;quit;                                                 |  +---------+-----+-------+-------+ */
    /*                                   | ods html close;                                           |    Return to TOC (hyperlink)       */
    /*                                   |                                                           |                                    */
    /**************************************************************************************************************************************/

    /*                             _                         _
    / |  ___  __ _ ___    ___   __| |___    _____  _____ ___| |
    | | / __|/ _` / __|  / _ \ / _` / __|  / _ \ \/ / __/ _ \ |
    | | \__ \ (_| \__ \ | (_) | (_| \__ \ |  __/>  < (_|  __/ |
    |_| |___/\__,_|___/  \___/ \__,_|___/  \___/_/\_\___\___|_|
     _                   _
    (_)_ __  _ __  _   _| |_ ___
    | | `_ \| `_ \| | | | __/ __|
    | | | | | |_) | |_| | |_\__ \
    |_|_| |_| .__/ \__,_|\__|___/
            |_|
    */

     INPUTS

     sashelp,class(where=(sex="F"))
     sashelp,class(where=(sex="M"))

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    title;
    footnote;

    %utlfkil(d:/xls/classtoc.xlsx);

    ods excel file="d:/xls/cynthia.xlsx" style=statistical;

    ods excel options(
          embedded_titles    = "yes"
          contents           = "yes"
          embedded_footnotes = "yes");

    footnote
      link="#'The Table of Contents'!a1"  "Return to TOC";
    run;quit;

    ods excel options(sheet_name="MALES");
    ods proclabel= "Detail Report of Males";

    title "Male Students";
    proc print data=sashelp.class
      (where=(sex="M"))
      contents="Demographics";
    run;

    ods excel options(sheet_name="FEMALES");
    ods proclabel= "Detail Report of Females";

    title "Female Students";
    proc print data=sashelp.class
      (where=(sex="F"))
      contents="Demographics";
    run;quit;

    ods excel close;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*    +----------------------------+                                                                                      */
    /*    |                  A         |                                                                                      */
    /*    |------------------+---------|                                                                                      */
    /*  1 |Detail Report of Males      |                                                                                      */
    /*    |----------------------------+                                                                                      */
    /*  2 |  Demographics (HYPERLINK)  |                                                                                      */
    /*    +------------------+---------+                                                                                      */
    /*  3 |Detail Report of Females    |                                                                                      */
    /*    |----------------------------+                                                                                      */
    /*  4 |  Demographics (HYPERLINK)  |                                                                                      */
    /*    +------------------+---------+                                                                                      */
    /*                                                                                                                        */
    /*  [Table of Contehts]                                                                                                   */
    /*                                                                                                                        */
    /*    ----------------------------------+                                                                                 */
    /*    |     A   |  B  |  C    |    D    |                                                                                 */
    /*    ----------------------------------+                                                                                 */
    /*  1 |NAME     | SEX |HEIGHT |  WEIGHT |                                                                                 */
    /*    +---------+-----+-------+---------+                                                                                 */
    /*  2 | ALFRED  |  M  |  69   |  112.5  |                                                                                 */
    /*    +---------+-----+-------+---------+                                                                                 */
    /*     ...                                                                                                                */
    /*    +---------+-----+-------+---------+                                                                                 */
    /*  N | WILLIAM |  M  | 66.5  |  112    |                                                                                 */
    /*    +---------+-----+-------+---------+                                                                                 */
    /*                                                                                                                        */
    /*    Return to TOC (hyperlink)                                                                                           */
    /*                                                                                                                        */
    /*  [MALES]                                                                                                               */
    /*                                                                                                                        */
    /*    ---------------------------------+                                                                                  */
    /*    |     A   |  B  |  C    |   D    |                                                                                  */
    /*    ---------------------------------+                                                                                  */
    /*  1 | NAME    | SEX |HEIGHT | WEIGHT |                                                                                  */
    /*    +---------+-----+-------+--------+                                                                                  */
    /*  2 | ALICE   |  F  |  69   | 112.5  |                                                                                  */
    /*    +---------+-----+-------+--------+                                                                                  */
    /*                                                                                                                        */
    /*    +---------+-----+-------+--------+                                                                                  */
    /*  N | BARBARA |  F  | 66.5  | 112    |                                                                                  */
    /*    +---------+-----+-------+--------+                                                                                  */
    /*                                                                                                                        */
    /*    Return to TOC (hyperlink)                                                                                           */
    /*                                                                                                                        */
    /*  [FEMALES]                                                                                                             */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___              _                 _  __
    |___ \    ___   __| |___   _ __   __| |/ _|
      __) |  / _ \ / _` / __| | `_ \ / _` | |_
     / __/  | (_) | (_| \__ \ | |_) | (_| |  _|
    |_____|  \___/ \__,_|___/ | .__/ \__,_|_|
     _                   _    |_|
    (_)_ __  _ __  _   _| |_ ___
    | | `_ \| `_ \| | | | __/ __|
    | | | | | |_) | |_| | |_\__ \
    |_|_| |_| .__/ \__,_|\__|___/
            |_|
    */

    data have;
      retain count 1;
      set sashelp.class ;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* COUNT NAME    SEX AGE HEIGHT WEIGHT                                                                                    */
    /*                                                                                                                        */
    /*   1   Alfred   M   14  69.0   112.5                                                                                    */
    /*   1   Alice    F   13  56.5    84.0                                                                                    */
    /*   1   Barbara  F   13  65.3    98.0                                                                                    */
    /*   1   Carol    F   14  62.8   102.5                                                                                    */
    /*   1   Henry    M   14  63.5   102.5                                                                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    %utlfkil(d:/pdf/want.pdf);

    title;
    footnote;

    ods escapechar="^";

    ods pdf file="d:/pdf/want.pdf" contents ;

    ods proclabel="Male Participants";
    title "Male Students";
     proc report nowd data=have
        (where=(sex="M")) contents="Demographics";
        col count name age height weight;
        define count / group noprint;
         break before count / contents="" page;
        compute after;
         lyn = "^S={URL='anchor.pdf#PAGE=1'
             color=blue
             just=left}Return to TOC" ;
         line lyn $64.;
        endcomp;
     run;

    ods proclabel="Female Participants";
    title "Female Students";
     proc report nowd data=have
        (where=(sex="F")) contents="Demographics";
        col count name age height weight;
        define count / group noprint;
         break before count / contents="" page;
        compute after;
         lyn = "^S={URL='anchor.pdf#PAGE=1'
             color=blue
             just=left }Return to TOC" ;
         line lyn $64.;
        endcomp;
     run;

    ods pdf close;


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  ------- Table of Contents -------                                                                                     */
    /*                                                                                                                        */
    /*  Table of Contents                                                                                                     */
    /*  Male Participants   .  .  .  .  . 1                                                                                   */
    /*  Demographics        .  .  .  .  . 1                                                                                   */
    /*  Female Participants .  .  .  .  . 2                                                                                   */
    /*  Demographics        .  .  .  .  . 2                                                                                   */
    /*                                                                                                                        */
    /*  Male Students                                                                                                         */
    /*                                                                                                                        */
    /*  NAME            AGE     HEIGHT     WEIGHT                                                                             */
    /*                                                                                                                        */
    /*  Alfred           14         69      112.5                                                                             */
    /*  Henry            14       63.5      102.5                                                                             */
    /*  James            12       57.3         83                                                                             */
    /*  Jeffrey          13       62.5         84                                                                             */
    /*  John             12         59       99.5                                                                             */
    /*  Philip           16         72        150                                                                             */
    /*  Robert           12       64.8        128                                                                             */
    /*                                                                                                                        */
    /*  Return to TOC                                                                                                         */
    /*                                                                                                                        */
    /*  Male Students                                                                                                         */
    /*                                                                                                                        */
    /*  NAME            AGE     HEIGHT     WEIGHT                                                                             */
    /*  Alice            13       56.5         84                                                                             */
    /*  Barbara          13       65.3         98                                                                             */
    /*  Carol            14       62.8      102.5                                                                             */
    /*  Jane             12       59.8       84.5                                                                             */
    /*  Janet            15       62.5      112.5                                                                             */
    /*  Joyce            11       51.3       50.5                                                                             */
    /*                                                                                                                        */
    /*  Return to TOC                                                                                                         */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____             _       _     _             _   _
    |___ /    ___   __| |___  | |__ | |_ _ __ ___ | | | |_ ___   ___
      |_ \   / _ \ / _` / __| | `_ \| __| `_ ` _ \| | | __/ _ \ / __|
     ___) | | (_) | (_| \__ \ | | | | |_| | | | | | | | || (_) | (__
    |____/   \___/ \__,_|___/ |_| |_|\__|_| |_| |_|_|  \__\___/ \___|
     _                   _
    (_)_ __  _ __  _   _| |_ ___
    | | `_ \| `_ \| | | | __/ __|
    | | | | | |_) | |_| | |_\__ \
    |_|_| |_| .__/ \__,_|\__|___/
            |_|
    */

    data have;
      retain count 1;
      set sashelp.class ;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* COUNT NAME    SEX AGE HEIGHT WEIGHT                                                                                    */
    /*                                                                                                                        */
    /*   1   Alfred   M   14  69.0   112.5                                                                                    */
    /*   1   Alice    F   13  56.5    84.0                                                                                    */
    /*   1   Barbara  F   13  65.3    98.0                                                                                    */
    /*   1   Carol    F   14  62.8   102.5                                                                                    */
    /*   1   Henry    M   14  63.5   102.5                                                                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    title;
    foornote;

    %utlfkil(d:/pages/toc.html);
    %utlfkil(d:/pages/males.html);
    %utlfkil(d:/pages/feales.htm);

    title "---- Table of Contents ----";
    ods escapechar="^";
    ods html body="toc.html" path="d:/pages";
    ods text="<a href='d:/pages/females.html'>
     List of Female Students</a>";
    ods text="<a href='d:/pages/males.html'>
     List of Male Students</a>";
    ods html close;

    ods html body="males.html" path="d:/pages";
    title "Male Students";
    proc report data=sashelp.class(where=(sex="M"));
     compute after;
      lyn =
      "^{style [URL='d:/pages/toc.html']Table of Contents}";
      line lyn $64.;
     endcomp;
    run;quit;

    ods html body="females.html" path="d:/pages";
    title "Female Students";
    proc report data=sashelp.class(where=(sex="F"));
     compute after;
      lyn =
       "^{style [URL='d:/pages/toc.html']Table of Contents}";
      line lyn $64.;
     endcomp;
    run;quit;
    ods html close;

    /**************************************************************************************************************************************/
    /*                                                                                                                                    */
    /* ---- Table od Contents ----                                                                                                        */
    /*                                                                                                                                    */
    /* List of Female Students                                                                                                            */
    /* List of Female Students                                                                                                            */
    /*                                                                                                                                    */
    /*                                                                                                                                    */
    /*  MALE STUDENTS                                                                                                                     */
    /*                                                                                                                                    */
    /*  +-------------------------------+                                                                                                 */
    /*  |NAME     | SEX |HEIGHT | WEIGHT|                                                                                                 */
    /*  +---------+-----+-------+-------+                                                                                                 */
    /*  | ALFRED  |  M  |  69   | 112.5 |                                                                                                 */
    /*  +---------+-----+-------+-------+                                                                                                 */
    /*   ...                                                                                                                              */
    /*  +---------+-----+-------+-------+                                                                                                 */
    /*  | WILLIAM |  M  | 66.5  | 112   |                                                                                                 */
    /*  +---------+-----+-------+-------+                                                                                                 */
    /*  | Return to Tabke of Contents   |                                                                                                 */
    /*  +---------+-----+-------+-------+                                                                                                 */
    /*                                                                                                                                    */
    /*                                                                                                                                    */
    /*                                                                                                                                    */
    /*  FEMALE STUDENTS                                                                                                                   */
    /*                                                                                                                                    */
    /*  +-------------------------------+                                                                                                 */
    /*  | NAME    | SEX |HEIGHT | WEIGHT|                                                                                                 */
    /*  +---------+-----+-------+-------+                                                                                                 */
    /*  | ALICE   |  F  |  69   | 112.5 |                                                                                                 */
    /*  +---------+-----+-------+-------+                                                                                                 */
    /*                                                                                                                                    */
    /*  +---------+-----+-------+-------+                                                                                                 */
    /*   | BARBARA |  F  | 66.5  | 112   |                                                                                                */
    /*  +---------+-----+-------+-------+                                                                                                 */
    /*  | Return to Tabke of Contents   |                                                                                                 */
    /*  +---------+-----+-------+-------+                                                                                                 */
    /*    Return to TOC (hyperlink)                                                                                                       */
    /*                                                                                                                                    */
    /**************************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

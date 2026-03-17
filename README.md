# utl-altair-slc-language3-proc-r-read-write-csv-files-and-summarize-and-looping-with-sqlite
Altair slc language3 proc r read write csv files and summarize and looping with sqlite
    %let pgm=utl-altair-slc-language3-proc-r-read-write-csv-files-and-summarize-and-looping-with-sqlite;

    %stop_submission;

    Altair slc language3 proc r read write csv files and summarize and looping with sqlite

    Note: SQLite has CSV read and write commands; however, I want to handle general text processing in SQL.
      Keep in mind that I am demonstrating the exact sqlite queries 9 languages below.
      In addition, you can use the exact same queries on any ODBC-compliant language or operating system.

    Too long to post on a list, see github
    https://github.com/rogerjdeangelis/utl-altair-slc-language3-proc-r-read-write-csv-files-and-summarize-and-looping-with-sqlite

    related repos (see for information of installing odbc and sqlite)

    https://github.com/rogerjdeangelis/utl-altair-slc-sqlite-cheat-sheet
    https://github.com/rogerjdeangelis/utl-altair-slc-language1-drop-down-to-open-source-spss-and-execute-postgresql-query
    https://github.com/rogerjdeangelis/utl-altair-slc-language2-drop-down-to-open-source-matlab-and-execute-sqlite-with-extensions

    PROBLEM

      PROCESS

      1  slc create sqlite table 'have' with 3 lines (sentences) and column name line

         d:/sqlite/mysqlite.db table have
         line

         This is the 1st line
         This is the 2nd line
         This is the 3rd line

      2  r summarize sqlite table

         select sex avg(age) avg(height) from have group by sex


      3  r convert sqlite table 'have' to text file using sqlite 'writefile' command

         d:/txt/have.txt

         This is the 1st line
         This is the 2nd line
         This is the 3rd line

      4  r convert text file 'd:/txt/have.txt' to r dataframe using sqlite readfile

          text

          This is the 1st line
          This is the 2nd line
          This is the 3rd line

      5  iterate(loop) over numbers 1-10 and output median (5.5)


    OBJECTIVE

      I am trying to make sql programmers expert programmers in
      9 languages using exactly the same sql queries.
      Use packages and procedures for analysis and sql for data wrangling and interfacing.

      Add very powerfull sql processing to the open source spss
      Posgresql has windows extensions.

      I hope to add repos with  drop downs to sql with windows extensions in many languages

     *language 1   open source spss
     *language 2   open source matlab
     *language 3   r
      language 4   python
      language 5   altair odbc sqlite
      language 6   excel
      language 7   perl
      language 8   slc proc sql (the only solution that does not support windows extensions)
      language 9   powershell

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    * best first;
    %utlfkil(d:/sqlite/mysqlite.db);

    libname workx sas7bdat "d:/wpswrkx"; /*---  put in autoexec ---*/

    proc datasets lib=workx kill;
    run;

    libname sqlite odbc noprompt="driver=sqlite3 odbc driver; database=d:/sqlite/mysqlite.db;LoadExt=d:/dll/sqlean.dll;";

    proc datasets lib=sqlite;
     delete have;
    run;

    options validvarname=v7;
    data sqlite.have workx.have;
      informat
        line    $24.
        name    $8.
        sex     $1.
        age     8.
        height  8.
        ;
     input name sex age height line &;
    cards4;
    Alfred M 14 69 This is the 1st line
    Alice F 13 56.5 This is the 2nd line
    Barbara F 13 65.3 This is the 3rd line
    Carol F 14 62.8 This is the 4th line
    Henry M 14 63.5 This is the 5th line
    ;;;;
    run;quit;

    proc contents data=sqlite.have;
    run;

    proc print data=sqlite.have;
    run;

    proc sql;
     SELECT sql FROM sqlite.sqlite_master WHERE name='have'
    ;quit;

    libname sqlite clear;

    /**************************************************************************************************************************/
    /* sqlite table have in database d:/sqlite/mysqlite.db                                                                    */
    /*                                                                                                                        */
    /* sqlite.have                                                                                                            */
    /*                                                                                                                        */
    /* line                        name        sex    age    height                                                           */
    /*                                                                                                                        */
    /* This is the 1st line        Alfred       M      14     69.0                                                            */
    /* This is the 2nd line        Alice        F      13     56.5                                                            */
    /* This is the 3rd line        Barbara      F      13     65.3                                                            */
    /* This is the 4th line        Carol        F      14     62.8                                                            */
    /* This is the 5th line        Henry        M      14     63.5                                                            */
    /*                                                                                                                        */
    /* sqlite table have contents                                                                                             */
    /*                                                                                                                        */
    /* CREATE TABLE have( line VARCHAR(24), name VARCHAR(8), sex VARCHAR(1), age DOUBLE PRECISION, height DOUBLE PRECISION )  */
    /*                                                                                                                        */
    /* Altair SLC                                                                                                             */
    /*                                                                                                                        */
    /* The CONTENTS Procedure                                                                                                 */
    /*                                                                                                                        */
    /* Data Set Name           HAVE                                                                                           */
    /* Member Type             VIEW                                                                                           */
    /* Engine                                                                                                                 */
    /* Observations            .                                                                                              */
    /* Variables               5                                                                                              */
    /* Indexes                 0                                                                                              */
    /* Observation Length      49                                                                                             */
    /* Deleted Observations    0                                                                                              */
    /* Data Set Type                                                                                                          */
    /* Label                                                                                                                  */
    /* Compressed              NO                                                                                             */
    /* Sorted                  NO                                                                                             */
    /* Data Representation                                                                                                    */
    /* Encoding                wlatin1 Windows-1252 Western                                                                   */
    /*                                                                                                                        */
    /*       Alphabetic List of Variables and Attributes                                                                      */
    /*                                                                                                                        */
    /* Number    Variable    Type  Len   Pos    Format Informat                                                               */
    /* ________________________________________________________                                                               */
    /*      4    age         Num     8    33                                                                                  */
    /*      5    height      Num     8    41                                                                                  */
    /*      1    line        Char   24     0    $24.   $24.                                                                   */
    /*      2    name        Char    8    24    $8.    $8.                                                                    */
    /*      3    sex         Char    1    32    $1.    $1.                                                                    */
    /**************************************************************************************************************************/

    /*                   _     _
    (_)_ __  _ __  _   _| |_  | | ___   __ _
    | | `_ \| `_ \| | | | __| | |/ _ \ / _` |
    | | | | | |_) | |_| | |_  | | (_) | (_| |
    |_|_| |_| .__/ \__,_|\__| |_|\___/ \__, |
            |_|                        |___/
    */

    1                                          Altair SLC         08:57 Tuesday, March 17, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ï»¿ods _all_ close;
               ^
    NOTE: AUTOEXEC processing completed

    1         * best first;
    2         %utlfkil(d:/sqlite/mysqlite.db);
    3
    4         libname workx sas7bdat "d:/wpswrkx"; /*---  put in autoexec ---*/
    NOTE: Library workx assigned as follows:
          Engine:        SAS7BDAT
          Physical Name: d:\wpswrkx


    Altair SLC

    The DATASETS Procedure

             Directory

    Libref           WORKX
    Engine           SAS7BDAT
    Physical Name    d:\wpswrkx

                                     Members

                                Member
      Number    Member Name     Type         File Size      Date Last Modified

    --------------------------------------------------------------------------

           1    AVGS            DATA              5120      17MAR2026:08:51:42
           2    HAVE            DATA              9216      17MAR2026:08:25:10
           3    MEDIAN_VALUE    DATA              5120      17MAR2026:08:51:42
    5
    6         proc datasets lib=workx kill;
    7         run;
    NOTE: Deleting WORKX.avgs (type=DATA)
    NOTE: Deleting WORKX.have (type=DATA)
    NOTE: Deleting WORKX.median_value (type=DATA)
    8
    9         libname sqlite odbc noprompt=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX;
    NOTE: Library sqlite assigned as follows:
          Engine:        ODBC
          Physical Name:  (SQLite version 3.43.2)

    NOTE: Procedure datasets step took :
          real time : 0.116
          cpu time  : 0.031



    Altair SLC

    The DATASETS Procedure

          Directory

    Libref         SQLITE
    Engine         ODBC
    Data Source
    10
    11        proc datasets lib=sqlite;
    NOTE: No matching members in directory
    12         delete have;
    13        run;
    NOTE: SQLITE.HAVE (memtype="DATA") was not found, and has not been deleted
    14
    15        options validvarname=v7;
    NOTE: Procedure datasets step took :
          real time : 0.021
          cpu time  : 0.015


    16        data sqlite.have workx.have;
    17          informat
    18            line    $24.
    19            name    $8.
    20            sex     $1.
    21            age     8.
    22            height  8.
    23            ;
    24         input name sex age height line &;
    25        cards4;

    NOTE: Data set "SQLITE.have" has an unknown number of observation(s) and 5 variable(s)
    NOTE: Data set "WORKX.have" has 5 observation(s) and 5 variable(s)
    NOTE: The data step took :
          real time : 0.131
          cpu time  : 0.000


    26        Alfred M 14 69 This is the 1st line
    27        Alice F 13 56.5 This is the 2nd line
    28        Barbara F 13 65.3 This is the 3rd line
    29        Carol F 14 62.8 This is the 4th line
    30        Henry M 14 63.5 This is the 5th line
    31        ;;;;
    32        run;quit;
    33
    34        proc contents data=sqlite.have;
    35        run;
    NOTE: Procedure contents step took :
          real time : 0.048
          cpu time  : 0.046


    36
    37        proc print data=sqlite.have;
    38        run;
    NOTE: 5 observations were read from "SQLITE.have"
    NOTE: Procedure print step took :
          real time : 0.013
          cpu time  : 0.000


    39
    40        proc sql;
    41         SELECT sql FROM sqlite.sqlite_master WHERE name='have'
    42        ;quit;
    WARNING: truncating character column type to 1024 characters long, based on dbmax_text setting.
    WARNING: truncating character column name to 1024 characters long, based on dbmax_text setting.
    WARNING: truncating character column tbl_name to 1024 characters long, based on dbmax_text setting.
    WARNING: truncating character column sql to 1024 characters long, based on dbmax_text setting.
    WARNING: truncating character column sql to 1024 characters long, based on dbmax_text setting.
    NOTE: Procedure sql step took :
          real time : 0.017
          cpu time  : 0.000


    NOTE: Libref SQLITE has been deassigned.
    43
    44        libname sqlite clear;
    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 0.446
          cpu time  : 0.187
    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    /*--- we read and write files using just sqlite queries ---*/
    %utlfk il(d:/txt/class_export.txt);

    options set=RHOME "C:\Progra~1\R\R-4.5.2\bin\r";

    proc r;
    export data=workx.have r=havex;
    submit;

    library(sqldf)
    options(sqldf.dll = "d:/dll/sqlean.dll")

    # summarize have table
    avgs <- sqldf('
        select
           sex,
           count(*) as count,
           round(avg(age),1)    as avg_age,
           round(avg(height),1) as avg_height
        from
           havex
        group
           by sex
        ');
    avgs

    db_path <- "d:/sqlite/mysqlite.db"

    # show that sqlite exists
    sqldf(c("SELECT sql FROM sqlite_master WHERE name='have'"), dbname = db_path)

    # create file d:/txt/class_export.txt uning lines column
    sqldf(c(
      "SELECT writefile(
         'd:/txt/class_export.txt',
         (SELECT group_concat(line, '\n') FROM have)
       )"
    ), dbname = db_path)

    # read back d:/txt/class_export.txt and create lines dataframe
    lines <- sqldf(c(
      "
      SELECT value AS txt
      FROM json_each('[\"' || replace(readfile('d:/txt/class_export.txt'), CHAR(10), '\",\"') || '\"]')
      "
    ), dbname = ":memory:")

    str(lines)
    print(lines)

    # loop through numbers 1-10 and compute the median
    median_value <- sqldf("
      WITH RECURSIVE nums(x) AS (
        SELECT 1
        UNION ALL
        SELECT x + 1 FROM nums WHERE x < 10
      ),
      med AS (
        SELECT
          x,
          ROW_NUMBER() OVER (ORDER BY x) AS r,
          COUNT(*) OVER () AS c
        FROM nums
      )
      SELECT AVG(x) AS median
      FROM med
      WHERE r IN ((c+1)/2, (c+2)/2)
    ")

    median_value

    print(paste("Median of 1-10:", median_value$median))
    endsubmit;
    import r=avgs data=workx.avgs;
    import r=median_value data=workx.median_value;
    run;

    proc print data=workx.avgs;
    run;

    proc print data=workx.median_value;
    run;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* SUMMARIZE SQLITE TABLE HAVE USING A SQLITE QUERY (ECACT CODE WORKS IN 9 languages)                                     */
    /* ----------------------------------------------------------------------------------                                     */
    /*                                                                                                                        */
    /*   sex count avg_age avg_height                                                                                         */
    /*                                                                                                                        */
    /* 1   F     3    13.3       61.5                                                                                         */
    /* 2   M     2    14.0       66.3                                                                                         */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* WRITE SQLITE TABLE HAVE TO A TEXT FILE USING SQLITE QUERY                                                              */
    /* ----------------------------------------------------------                                                             */
    /*                                                                                                                        */
    /* d:/txt/class_export.txt                                                                                                */
    /*                                                                                                                        */
    /* This is the 1st line                                                                                                   */
    /* This is the 2nd line                                                                                                   */
    /* This is the 3rd line                                                                                                   */
    /* This is the 4th line                                                                                                   */
    /* This is the 5th line                                                                                                   */
    /*                                                                                                                        */
    /* READ THE TEXT FILE USING SQLITE QUERY AND OUTPUT R DATAFRAME                                                           */
    /* -------------------------------------------------------------                                                          */
    /*                                                                                                                        */
    /* 'data.frame':      5 obs. of  1 variable:                                                                              */
    /*  $ txt: chr  "This is the 1st line" "This is the 2nd line" "This is the 3rd line" "This is the 4th line" ...           */
    /*                                                                                                                        */
    /* R DATAFRAME lines                                                                                                      */
    /*                    txt                                                                                                 */
    /* 1 This is the 1st line                                                                                                 */
    /* 2 This is the 2nd line                                                                                                 */
    /* 3 This is the 3rd line                                                                                                 */
    /* 4 This is the 4th line                                                                                                 */
    /* 5 This is the 5th line                                                                                                 */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* USING SQLITE QUERY LOOP THOUGH AUTOGENERATES NUMBERS 1-10 AND COMPUTE THE MEDIAN                                       */
    /* --------------------------------------------------------------------------------                                       */
    /*                                                                                                                        */
    /* [1] "Median of 1-10: 5.5"                                                                                              */
    /*                                                                                                                        */
    /* R dataframe median_value                                                                                               */
    /*                                                                                                                        */
    /*   median                                                                                                               */
    /* 1    5.5                                                                                                               */
    /*                                                                                                                        */
    /* BACK TO THE SLC OUTPUT                                                                                                 */
    /* ----------------------                                                                                                 */
    /*                                                                                                                        */
    /* Altair SLC                                                                                                             */
    /*                                                                                                                        */
    /* Obs    SEX    COUNT    AVG_AGE    AVG_HEIGHT                                                                           */
    /*                                                                                                                        */
    /*  1      F       3        13.3        61.5                                                                              */
    /*  2      M       2        14.0        66.3                                                                              */
    /*                                                                                                                        */
    /* Altair SLC                                                                                                             */
    /*                                                                                                                        */
    /* Obs    MEDIAN                                                                                                          */
    /*                                                                                                                        */
    /*  1       5.5                                                                                                           */
    /**************************************************************************************************************************/

    /*                                   _
     _ __  _ __ ___   ___ ___  ___ ___  | | ___   __ _
    | `_ \| `__/ _ \ / __/ _ \/ __/ __| | |/ _ \ / _` |
    | |_) | | | (_) | (_|  __/\__ \__ \ | | (_) | (_| |
    | .__/|_|  \___/ \___\___||___/___/ |_|\___/ \__, |
    |_|                                          |___/
    */

    1                                          Altair SLC         08:51 Tuesday, March 17, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ï»¿ods _all_ close;
               ^
    ERROR: Expected a statement keyword : found "?"

    NOTE: AUTOEXEC processing completed

    1         /*--- we read and write files using just sqlite queries ---*/
    2         %utlfk il(d:/txt/class_export.txt);
    WARNING: Apparent invocation of macro "utlfk" not resolved
    ERROR: Expected a statement keyword : found "%"
    3
    4         options set=RHOME "C:\Progra~1\R\R-4.5.2\bin\r";
    5
    6         proc r;
    NOTE: Using R version 4.5.2 (2025-10-31 ucrt) from C:\Program Files\R\R-4.5.2
    7         export data=workx.have r=havex;
    NOTE: Creating R data frame 'havex' from data set 'WORKX.have'

    8         submit;
    9
    10        library(sqldf)
    11        options(sqldf.dll = "d:/dll/sqlean.dll")
    12
    13        # summarize have table
    14        avgs <- sqldf('
    15            select
    16               sex,
    17               count(*) as count,
    18               round(avg(age),1)    as avg_age,
    19               round(avg(height),1) as avg_height
    20            from
    21               havex
    22            group
    23               by sex
    24            ');
    25        avgs
    26
    27        db_path <- "d:/sqlite/mysqlite.db"
    28
    29        # show that sqlite exists
    30        sqldf(c("SELECT sql FROM sqlite_master WHERE name='have'"), dbname = db_path)
    31
    32        # create file d:/txt/class_export.txt uning lines column
    33        sqldf(c(
    34          "SELECT writefile(
    35             'd:/txt/class_export.txt',
    36             (SELECT group_concat(line, '\n') FROM have)
    37           )"
    38        ), dbname = db_path)
    39
    40        # read back d:/txt/class_export.txt and create lines dataframe
    41        lines <- sqldf(c(
    42          "
    43          SELECT value AS txt
    44          FROM json_each('[\"' || replace(readfile('d:/txt/class_export.txt'), CHAR(10), '\",\"') || '\"]')
    45          "
    46        ), dbname = ":memory:")
    47
    48        str(lines)
    49        print(lines)
    50
    51        # loop through numbers 1-10 and compute the median
    52        median_value <- sqldf("
    53          WITH RECURSIVE nums(x) AS (
    54            SELECT 1
    55            UNION ALL
    56            SELECT x + 1 FROM nums WHERE x < 10
    57          ),
    58          med AS (
    59            SELECT
    60              x,
    61              ROW_NUMBER() OVER (ORDER BY x) AS r,
    62              COUNT(*) OVER () AS c
    63            FROM nums
    64          )
    65          SELECT AVG(x) AS median
    66          FROM med
    67          WHERE r IN ((c+1)/2, (c+2)/2)
    68        ")
    69
    70        median_value
    71
    72        print(paste("Median of 1-10:", median_value$median))
    73        endsubmit;

    NOTE: Submitting statements to R:

    >
    > library(sqldf)
    Loading required package: gsubfn
    Loading required package: proto
    Loading required package: RSQLite
    > options(sqldf.dll = "d:/dll/sqlean.dll")
    >
    > # summarize have table
    > avgs <- sqldf('
    +     select
    +        sex,
    +        count(*) as count,
    +        round(avg(age),1)    as avg_age,
    +        round(avg(height),1) as avg_height
    +     from
    +        havex
    +     group
    +        by sex
    +     ');
    > avgs
    >
    > db_path <- "d:/sqlite/mysqlite.db"
    >
    > # show that sqlite exists
    > sqldf(c("SELECT sql FROM sqlite_master WHERE name='have'"), dbname = db_path)
    >
    > # create file d:/txt/class_export.txt uning lines column
    > sqldf(c(
    +   "SELECT writefile(
    +      'd:/txt/class_export.txt',
    +      (SELECT group_concat(line, '\n') FROM have)
    +    )"
    + ), dbname = db_path)
    >
    > # read back d:/txt/class_export.txt and create lines dataframe
    > lines <- sqldf(c(
    +   "
    +   SELECT value AS txt
    +   FROM json_each('[\"' || replace(readfile('d:/txt/class_export.txt'), CHAR(10), '\",\"') || '\"]')
    +   "
    + ), dbname = ":memory:")
    >
    > str(lines)
    > print(lines)
    >
    > # loop through numbers 1-10 and compute the median
    > median_value <- sqldf("
    +   WITH RECURSIVE nums(x) AS (
    +     SELECT 1
    +     UNION ALL
    +     SELECT x + 1 FROM nums WHERE x < 10
    +   ),
    +   med AS (
    +     SELECT
    +       x,
    +       ROW_NUMBER() OVER (ORDER BY x) AS r,
    +       COUNT(*) OVER () AS c
    +     FROM nums
    +   )
    +   SELECT AVG(x) AS median
    +   FROM med
    +   WHERE r IN ((c+1)/2, (c+2)/2)
    + ")
    >
    > median_value
    >
    > print(paste("Median of 1-10:", median_value$median))

    NOTE: Processing of R statements complete

    74        import r=avgs data=workx.avgs;
    NOTE: Creating data set 'WORKX.avgs' from R data frame 'avgs'
    NOTE: Column names modified during import of 'avgs'
    NOTE: Data set "WORKX.avgs" has 2 observation(s) and 4 variable(s)

    75        import r=median_value data=workx.median_value;
    NOTE: Creating data set 'WORKX.median_value' from R data frame 'median_value'
    NOTE: Column names modified during import of 'median_value'
    NOTE: Data set "WORKX.median_value" has 1 observation(s) and 1 variable(s)

    76        run;
    NOTE: Procedure r step took :
          real time : 1.573
          cpu time  : 0.062


    77
    78        proc print data=workx.avgs;
    79        run;
    NOTE: 2 observations were read from "WORKX.avgs"
    NOTE: Procedure print step took :
          real time : 0.006
          cpu time  : 0.000


    80
    81        proc print data=workx.median_value;
    82        run;
    NOTE: 1 observations were read from "WORKX.median_value"
    NOTE: Procedure print step took :
          real time : 0.013
          cpu time  : 0.000


    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 1.671
          cpu time  : 0.109

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

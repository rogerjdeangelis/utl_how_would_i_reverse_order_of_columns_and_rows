# utl_how_would_i_reverse_order_of_columns_and_rows
How would I Reverse Order of Columns and Rows. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverfl SAS community.
    How would I Reverse Order of Columns and Rows

    github
    https://tinyurl.com/y8f3jxwa
    https://github.com/rogerjdeangelis/utl_how_would_i_reverse_order_of_columns_and_rows

    see
    https://tinyurl.com/y8b7laak
    https://communities.sas.com/t5/Base-SAS-Programming/How-would-I-Reverse-Order-of-All-Variables-Rows-and-Columns/m-p/443631

    INPUT
    =====

      SASHELP.CLASS total obs=19

        Obs    NAME       SEX    AGE    HEIGHT    WEIGHT

          1    Alfred      M      14     69.0      112.5
          2    Alice       F      13     56.5       84.0
          3    Barbara     F      13     65.3       98.0
         ....
         17    Ronald      M      15     67.0      133.0
         18    Thomas      M      11     57.5       85.0
         19    William     M      15     66.5      112.0


    WANT
    ====

      WORK.WANT total obs=19

              Last                              First
              Column                            Column

       Obs    WEIGHT    HEIGHT    AGE    SEX    NAME

         1     112.0     66.5      15     M     William   ** last ob
         2      85.0     57.5      11     M     Thomas
         3     133.0     67.0      15     M     Ronald
         .......
        17      98.0     65.3      13     F     Barbara
        18      84.0     56.5      13     F     Alice
        19     112.5     69.0      14     M     Alfred    ** first ob


    PROCESS
    =======

       data want;

         if _n_=0 then do;

            %let rc=dosubl('
                 * dictionaries are too slow;
                 ods output position=havPos;
                 proc contents data=sashelp.class position;
                 run;quit;
                 proc sql;
                    select variable into :vars separated by " "
                    from havPos
                    order by num descending
                 ;quit;
            '));
          end;

          retain &vars;
          do i=nobs to 1 by -1;
             set sashelp.class nobs=nobs point=i;
             output;
          end;
          stop;

       run;quit;

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

      Just use sashelp.class

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    data want;

      if _n_=0 then do;

         %let rc=dosubl('
              * dictionaries are too slow;
              ods output position=havPos;
              proc contents data=sashelp.class position;
              run;quit;
              proc sql;
                 select variable into :vars separated by " "
                 from havPos
                 order by num descending
              ;quit;
         '));
       end;

       retain &vars;
       do i=nobs to 1 by -1;
          set sashelp.class nobs=nobs point=i;
          output;
       end;
       stop;

    run;quit;

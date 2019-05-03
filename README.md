# utl-dynamic-were-statements-to-select-students-with-weight-less-than-johns
Dynamic were statements to select students with weight less than johns   
    Dynamic were statements to select students with weight less than johns                              
                                                                                                        
       Two Solutions                                                                                    
             1. Using DOSUBL and datastep inside where clause                                           
             2. Using DOSUBL and proc sql inside where clause                                           
    *_                   _                                                                              
    (_)_ __  _ __  _   _| |_                                                                            
    | | '_ \| '_ \| | | | __|                                                                           
    | | | | | |_) | |_| | |_                                                                            
    |_|_| |_| .__/ \__,_|\__|                                                                           
            |_|                                                                                         
    ;                                                                                                   
                                                                                                        
    Up to 40 obs from SASHELP.CLASS total obs=19                                                        
                                                                                                        
    Obs    NAME       SEX    AGE    HEIGHT    WEIGHT                                                    
                                                                                                        
      1    Alfred      M      14     69.0      112.5                                                    
      2    Alice       F      13     56.5       84.0                                                    
      3    Barbara     F      13     65.3       98.0                                                    
      4    Carol       F      14     62.8      102.5                                                    
      5    Henry       M      14     63.5      102.5                                                    
      6    James       M      12     57.3       83.0                                                    
      7    Jane        F      12     59.8       84.5                                                    
      8    Janet       F      15     62.5      112.5                                                    
      9    Jeffrey     M      13     62.5       84.0                                                    
                                                                                                        
     10    John        M      12     59.0       99.5  RULE select students with weight lt John          
                                                                                                        
     11    Joyce       F      11     51.3       50.5                                                    
     12    Judy        F      14     64.3       90.0                                                    
     13    Louise      F      12     56.3       77.0                                                    
     14    Mary        F      15     66.5      112.0                                                    
     15    Philip      M      16     72.0      150.0                                                    
     16    Robert      M      12     64.8      128.0                                                    
     17    Ronald      M      15     67.0      133.0                                                    
     18    Thomas      M      11     57.5       85.0                                                    
     19    William     M      15     66.5      112.0                                                    
                                                                                                        
                                                                                                        
    *            _               _                                                                      
      ___  _   _| |_ _ __  _   _| |_                                                                    
     / _ \| | | | __| '_ \| | | | __|                                                                   
    | (_) | |_| | |_| |_) | |_| | |_                                                                    
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                   
                    |_|                                                                                 
    ;                                                                                                   
                                                                                                        
    Up to 40 obs from WANT total obs=9                                                                  
                                             All less than 99.5                                         
                                                                                                        
    Obs    NAME       SEX    AGE    HEIGHT    WEIGHT                                                    
                                                                                                        
     1     Alice       F      13     56.5      84.0                                                     
     2     Barbara     F      13     65.3      98.0                                                     
     3     James       M      12     57.3      83.0                                                     
     4     Jane        F      12     59.8      84.5                                                     
     5     Jeffrey     M      13     62.5      84.0                                                     
     6     Joyce       F      11     51.3      50.5                                                     
     7     Judy        F      14     64.3      90.0                                                     
     8     Louise      F      12     56.3      77.0                                                     
     9     Thomas      M      11     57.5      85.0                                                     
                                                                                                        
    *          _       _   _                                                                            
     ___  ___ | |_   _| |_(_) ___  _ __  ___                                                            
    / __|/ _ \| | | | | __| |/ _ \| '_ \/ __|                                                           
    \__ \ (_) | | |_| | |_| | (_) | | | \__ \                                                           
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/                                                           
                                                                                                        
    ;                                                                                                   
                                                                                                        
                                                                                                        
    1. Using DOSUBL and datastep inside where clause                                                    
                                                                                                        
                                                                                                        
    %symdel john / nowarn;                                                                              
    data want;                                                                                          
                                                                                                        
      set sashelp.class(where=(weight lt %let rc=%sysfunc(dosubl('                                      
                                                                                                        
          data _null_;                                                                                  
             set sashelp.class(where=(name="John"));                                                    
             call symputx("john",weight);                                                               
          run;quit;                                                                                     
                                                                                                        
         '));                                                                                           
                                                                                                        
          &John                                                                                         
         ));                                                                                            
                                                                                                        
    run;quit;                                                                                           
                                                                                                        
                                                                                                        
    2. Using DOSUBL and proc sql inside where clause                                                    
                                                                                                        
    %symdel john / nowarn;                                                                              
    data want;                                                                                          
                                                                                                        
      set sashelp.class(where=(weight lt %let rc=%sysfunc(dosubl('                                      
                                                                                                        
          proc sql;                                                                                     
             select                                                                                     
                weight                                                                                  
             into                                                                                       
                :john trimmed                                                                           
             from                                                                                       
                sashelp.class                                                                           
             where                                                                                      
                name = "John"                                                                           
          ;quit;                                                                                        
                                                                                                        
         '));                                                                                           
                                                                                                        
          &John                                                                                         
                                                                                                        
         ));                                                                                            
                                                                                                        
    run;quit;                                                                                           
                                                                                                        
                                                                                                        
                                                                                                        

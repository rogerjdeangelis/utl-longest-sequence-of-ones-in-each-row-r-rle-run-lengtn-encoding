# utl-longest-sequence-of-ones-in-each-row-r-rle-run-lengtn-encoding
Longest sequence of ones in each row r rle run lengtn encoding 

    Longest sequence of ones in each row r rle run lengtn encoding                                                      
                                                                                                                        
    github                                                                                                              
    https://tinyurl.com/y2ynjfre                                                                                        
    https://github.com/rogerjdeangelis/utl-longest-sequence-of-ones-in-each-row-r-rle-run-lengtn-encoding               
                                                                                                                        
    github                                                                                                              
    https://tinyurl.com/yxa279x9                                                                                        
    https://communities.sas.com/t5/New-SAS-User/How-to-count-sequential-values-by-observation/m-p/591726                
                                                                                                                        
    related repos                                                                                                       
    https://tinyurl.com/y6nczpgy                                                                                        
    https://github.com/rogerjdeangelis?utf8=%E2%9C%93&tab=repositories&q=rle+in%3Areadme&type=&language=                
                                                                                                                        
    *_                   _                                                                                              
    (_)_ __  _ __  _   _| |_                                                                                            
    | | '_ \| '_ \| | | | __|                                                                                           
    | | | | | |_) | |_| | |_                                                                                            
    |_|_| |_| .__/ \__,_|\__|                                                                                           
            |_|                                                                                                         
    ;                                                                                                                   
                                                                                                                        
    options validvarname=upcase;                                                                                        
    libname sd1 "d:/sd1";                                                                                               
    data sd1.have;                                                                                                      
     input patid a b c d e ;                                                                                            
    cards4;                                                                                                             
    1 0 1 0 0 1                                                                                                         
    2 1 1 1 0 0                                                                                                         
    3 0 1 1 0 0                                                                                                         
    4 0 1 1 1 1                                                                                                         
    5 0 0 0 1 0                                                                                                         
    ;;;;                                                                                                                
    run;quit;                                                                                                           
                                                                                                                        
                          | RULES                                                                                       
     SD1.HAVE total obs=5 | =====                                                                                       
                          |                                                                                             
     PATID   A B C D E    | Longest lengths on 1s                                                                       
                          |                                                                                             
       1     0 1 0 0 1    | 1                                                                                           
                                                                                                                        
       2     1 1 1 0 0    | 3                                                                                           
       3     0 1 1 0 0    | 2                                                                                           
       4     0 1 1 1 1    | 4                                                                                           
       5     0 0 0 1 0    | 1                                                                                           
                                                                                                                        
    *            _               _                                                                                      
      ___  _   _| |_ _ __  _   _| |_                                                                                    
     / _ \| | | | __| '_ \| | | | __|                                                                                   
    | (_) | |_| | |_| |_) | |_| | |_                                                                                    
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                   
                    |_|                                                                                                 
    ;                                                                                                                   
                                                                                                                        
    WORK.WANT total obs=5                                                                                               
                                                                                                                        
      PATID   A B C D E   WANT                                                                                          
                                                                                                                        
        1     0 1 0 0 1    1                                                                                            
        2     1 1 1 0 0    3                                                                                            
        3     0 1 1 0 0    2                                                                                            
        4     0 1 1 1 1    4                                                                                            
        5     0 0 0 1 0    1                                                                                            
                                                                                                                        
    *                                                                                                                   
     _ __  _ __ ___   ___ ___  ___ ___                                                                                  
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                 
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                 
    | .__/|_|  \___/ \___\___||___/___/                                                                                 
    |_|                                                                                                                 
    ;                                                                                                                   
                                                                                                                        
    %utlfkil(d:/xpt/want.xpt);                                                                                          
                                                                                                                        
    %utl_submit_r64('                                                                                                   
      library(haven);                                                                                                   
      library(SASxport);                                                                                                
      have<-read_sas("d:/sd1/have.sas7bdat")[,-1];                                                                      
      want<-c();                                                                                                        
      for (i in (1:nrow(have))) {                                                                                       
         runs <- rle(have[i,]);                                                                                         
         tmp<-max(runs$lengths[runs$values==1]);                                                                        
         want=append(want,tmp);                                                                                         
      };                                                                                                                
      want<-as.data.frame(want);                                                                                        
      write.xport(want,file="d:/xpt/want.xpt");                                                                         
    ');                                                                                                                 
                                                                                                                        
    libname xpt xport "d:/xpt/want.xpt";                                                                                
    data want;                                                                                                          
      merge  sd1.have xpt.want;                                                                                         
    run;quit;                                                                                                           
    libname xpt clear;                                                                                                  
                                                                                                                        
    *_                                                                                                                  
    | | ___   __ _                                                                                                      
    | |/ _ \ / _` |                                                                                                     
    | | (_) | (_| |                                                                                                     
    |_|\___/ \__, |                                                                                                     
             |___/                                                                                                      
    ;                                                                                                                   
                                                                                                                        
    > library(haven);  library(SASxport);  have<-read_sas("d:/sd1/have.sas7bdat")[,-1];                                 
    > want<-c();  for (i in (1:nrow(have))) {     runs <- rle(have[i,]); tmp<-max(runs$l                                
    > lengths[runs$values==1]);     want=append(want,tmp);  };                                                          
    > want<-as.data.frame(want);  write.xport(want,file="d:/xpt/want.xpt");                                             
    >                                                                                                                   
    NOTE: 3 lines were written to file PRINT.                                                                           
    Stderr output:                                                                                                      
    package 'haven' was built under R version 3.5.3                                                                     
    NOTE: 2 records were read from the infile RUT.                                                                      
          The minimum record length was 2.                                                                              
          The maximum record length was 297.                                                                            
    NOTE: DATA statement used (Total process time):                                                                     
          real time           3.34 seconds                                                                              
          cpu time            0.04 seconds                                                                              
                                                                                                                        
                                                                                                                        
    NOTE: Fileref RUT has been deassigned.                                                                              
    NOTE: Fileref R_PGM has been deassigned.                                                                            
    590   libname xpt xport "d:/xpt/want.xpt";                                                                          
    NOTE: Libref XPT was successfully assigned as follows:                                                              
          Engine:        XPORT                                                                                          
          Physical Name: d:\xpt\want.xpt                                                                                
    591   data want;                                                                                                    
    592     merge  sd1.have xpt.want;                                                                                   
    593   run;                                                                                                          
                                                                                                                        
    NOTE: There were 5 observations read from the data set SD1.HAVE.                                                    
    NOTE: There were 5 observations read from the data set XPT.WANT.                                                    
    NOTE: The data set WORK.WANT has 5 observations and 7 variables.                                                    
    NOTE: DATA statement used (Total process time):                                                                     
          real time           0.01 seconds                                                                              
          cpu time            0.01 seconds                                                                              
                                                                                                                        
                                                                                                                        
    593 !     quit;                                                                                                     
    594   libname xpt clear;                                                                                            
    NOTE: Libref XPT has been deassigned.                                                                               
                                                                                                                        
                                                                                                                        

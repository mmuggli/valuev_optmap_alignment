Notes by Martin Muggli
======================
This git repo is for simple maintance/usability changes relative to Valuev et al.'s original software (the root commit in the DAG).

Their paper describes a number of alignment scoring parameters.  These appear to match to the follow constructor parameters of a scoring_params object as follows:

    scoring_params(double _mu,            //for old scoring
                   double _lambda,        //penalty for the missing restriction site  
                   double _nu,            //reward for each matched stretch of a map
                   int _delta,            //how much back in the scoring matrix you can trace
                      
                   double _distr_lambda,  //parameters for the
                   double _distr_sigma,   //length distribution
                      
                   double _zeta,          //average number of random breaks per Kb
                   double _dig_p,         //digestion rate
                   double _eta,           //the std for fragments below lo_fr_thresh
                      
                   double _lo_fr_thresh); //the size thresh below which the


contrib/soma_silico2valuev.py will convert from SOMA's in-silico digested file format (the actual file input to their match executable, also used by TWIN) to valuev's format

Valuev file format
------------------
Every sequence of fragments (either on the query or database side) consists of set of three lines:

First line:  Read Name (the entire line)
Second line: The Read (a list of whitespace separated fields; The first two are Enzyme Name and Enzyme Acronym respectively, the rest are double literals for the fragment sizes in Kbp)
Third line: Empty


For example, here is an optical map for Y.kristensenii digested with AflII:
    ---- <BOF> ----
    Y.kristensenii_AflII.map.opt
    enzyme enzyme  22.899  9.25  10.411  9.098  28.539  3.335  3.061  2.498  16.843  7.413  3.187  4.676  13.363  11.209  4.804  6.698  2.529  14.887  3.326  28.891  24.028  9.013  5.213  5.336  25.184  30.465  5.658  6.151  3.09  3.438  14.344  6.829  3.989  21.359  6.367  2.435  3.196  6.871  4.313  31.724  8.605  3.255  17.758  2.446  7.859  15.876  2.684  18.969  9.243  12.26  26.403  17.414  4.695  16.753  24.298  6.231  47.639  21.881  1.986  23.903  32.48  4.94  0.859  2.775  24.167  38.12  1.482  63.853  3.262  5.352  13.283  11.667  30.237  14.5  18.014  7.684  28.433  11.829  4.651  10.258  5.184  16.159  15.398  6.874  6.057  20.144  2.91  39.37  21.984  21.977  37.679  15.492  6.709  52.032  54.558  23.508  12.262  10.856  3.301  3.337  18.462  9.022  2.181  9.499  6.918  10.052  1.824  9.13  25.486  5.832  28.83  13.049  1.901  8.363  1.453  8.535  5.097  8.654  8.279  12.615  32.125  25.918  5.954  7.852  7.321  7.134  4.929  35.992  16.782  10.476  8.621  42.923  2.243  2.218  23.766  2.436  19.731  18.727  29.814  10.44  7.106  18.034  1.557  14.617  23.821  1.453  12.72  3.631  59.241  19.334  9.022  10.167  3.193  21.412  9.543  3.539  35.09  15.628  6.06  18.225  31.318  1.801  5.778  2.182  25.116  12.521  9.943  5.488  18.452  7.86  11.126  19.21  43.832  23.878  4.357  7.389  10.663  16.015  5.234  11.253  17.121  3.378  12.288  4.631  1.744  10.941  6.793  5.465  2.641  5.847  43.388  15.442  4.957  4.045  3.571  3.143  8.546  4.272  4.886  9.528  12.196  7.671  15.706  2.956  42.079  11.277  18.662  30.511  8.994  3.848  6.303  19.051  3.415  2.843  10.278  3.017  17.406  3.128  27.661  1.675  14.421  2.75  11.43  59.592  30.783  16.976  18.529  6.191  15.0  4.642  7.362  17.179  23.111  7.516  3.749  7.714  4.469  6.347  4.339  6.773  23.209  25.559  40.158  1.779  5.497  24.228  21.017  11.527  4.146  40.423  5.079  18.332  16.427  1.789  10.247  3.46  10.189  11.657  4.14  27.182  10.729  25.953  4.142  17.351  14.935  3.887  10.86  1.283  7.385  8.856  4.388  13.581  31.09  12.151  1.014  7.887  2.057  15.028  2.839  4.28  9.925  23.971  5.945  5.962  27.979  5.662  4.952  7.511  10.579  7.776  3.169  16.386  23.462  13.844  22.119  31.032  10.57  8.637  46.733  17.625  27.344  11.219  3.464  5.056  12.83  26.197  5.776  5.079  14.297  14.001  7.061  24.615  14.712  23.526  33.286  26.974  3.412  24.027  4.607  12.874  2.779  9.043  2.438  12.707  15.735  6.013  3.25  6.261  6.83  3.032  49.504  2.822  3.762  1.282  20.263  1.052  10.631  20.662  54.818  3.894  12.836  2.281  37.185  10.734  5.158  1.315  13.831  5.133  3.012  2.54 
    
    ----- <EOF> ---


And here are several in silico digested contigs in a separate file:
    ---- <BOF> ----
    NODE_1_length_84997_cov_11.5455_ID_1 84997 8
    enzyme enzyme 5.973 0.258 3.597 8.314 29.279 2.767 18.641 10.108
    
    NODE_2_length_84882_cov_11.9591_ID_3 84882 3
    enzyme enzyme 11.712 24.053 47.294
    
    NODE_3_length_83550_cov_12.8835_ID_5 83550 13
    enzyme enzyme 1.752 14.297 0.233 6.33 3.691 22.282 5.844 0.991 2.29 2.93 6.26 3.844 12.49
    ----- <EOF> ---


Valuev et al.'s original readme
===============================
This package contains the files for the fit alignment and overlap alignment as well as all necessary files to make alignment modifications you may need. 

Fit alignment: cd to ./fit directory and compile by g++ fit_mols_and_store_als.cc
Overlap alignment: cd to ./ovlp directory and compile by g++ ovlp.cc

This code comes with absolutely no warranty and is free for redistribution and use for non-commercial purposed only.
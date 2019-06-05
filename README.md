# Note to reviewers

This repository holds the source code and raw experimental results of ICDM 2019 paper DM251. This repository is for reviewing purposes only. All identity information of the authors has been hidden.

# How to use the code

The main file in this repository is HBOP.py under the Classification folder. It implements the HBOP algorithm and all its variants (see the "Impact of Design Choices" section in our paper). Note that only the full version of HBOP is timed. Also, our raw experimental results are in the Results folder.

To use the code, please keep all the packages and files in this repository in a single folder. First, change the path in line 18 of HBOP.py to your repository path. Then, run the following command in your command council.

    python.exe [full path of HBOP.py] [dataset name] [runId] [mother path of the dataset] [full path of the folder to save the results]

Here runId is used to distinguish between different runs on the same dataset.

For example, suppose you have saved the entire repository at G:\HBOP, and you wish to run HBOP on the sample dataset (FaceFour) included in our repository and save the outputs in the Results folder. In this case, please run the following command.

    python.exe G:\HBOP\Classification\HBOP.py FaceFour 0 G:/HBOP/Data G:/HBOP/Results  
    
Running HBOP.py will result in the following output files.

1. accuracies_[dataset name]_HBOP.[runId].txt

    This file shows the accuracies of 12 variants of HBOP, in the order of HBOP-NW, HBOP-NX-NW, HBOP-X-NW, HBOP-SAX-NW, HBOP-SAX-NX-NW, HBOP-SAX-X-NW, HBOP, HBOP-NX, HBOP-X, HBOP-SAX, HBOP-SAX-NX, HBOP-SAX-X.
    
2. time_[dataset name]_HBOP.[runId].txt

    This file shows the running time of the full version of HBOP. The four outputs are the dataset name, training time, classification time per example and accuracy.

Please note that due to implementation bias, in certain cases, the accuracies of the full version of HBOP in the "accuracies" file and the "time" file can be different. Fortunately, this only happened in very few cases in our experiments.
    
# How did we preprocess the data?

We have used datasets from the latest version of the UCR archive 

    Hoang Anh Dau, Eamonn Keogh, Kaveh Kamgar, Chin-Chia Michael Yeh, Yan Zhu, Shaghayegh Gharghabi , Chotirat Ann Ratanamahatana, Yanping Chen, Bing Hu, Nurjahan Begum, Anthony Bagnall , Abdullah Mueen and Gustavo Batista (2018). The UCR Time Series Classification Archive. URL https://www.cs.ucr.edu/~eamonn/time_series_data_2018/
    
For datasets with missing values, we followed the briefing document of the UCR archive, and filled the missing values with linear interpolation. For datasets with variable time series lengths, both HBOP and BOPF can in theory handle such cases directly. However, the original C++ implementation of BOPF demands the time series to be of the same length, thus we opt to conduct this procedure. The UCR  briefing document suggests padding with low amplitude random values. Instead, we choose to pad zeros. The reason why we make this choice is that the low amplitude values can be significantly amplified after z-normalization. For subsequence-based methods such as BOPF and our HBOP, this may significantly affect the results.

# How did we obtain the experimental results?

In our paper, we compared the classification accuracy of our HBOP method with three 1NN algorithms and BOPF. The classification error rates of the 1NN algorithms were drawn from the UCR archive webpage. For BOPF, we ran the original C++ code of BOPF (with minor modifications, see below) to obtain the results. All error rates were rounded to the nearest four decimal digits prior to comparison.

For the original C++ code of BOPF, we made several minor modifications to eliminate bugs. Concretely, these modifications are as follows:

1. Line 242 of the original code is 
    
        int i, j, k, p, maxK;
   which we have changed to
    
        int i, j, k, p, maxK = 0;

2. Line 320 of the original code is 

        int i, j, k, p, maxK;
    
    which we have changed to
     
        int i, j, k, p, maxK = 0;
        
3. Line 500 of the original code is

        r = r1*r1 / (r2*r3);
   
   which we have changed to
   
        if(r2 != 0)
            r = r1*r1 / (r2*r3);
        else
            r = 0;

As with efficiency, we compared the training time of HBOP and BOPF. We implemented BOPF with Python and used this implementation to obtain the training time of BOPF. Note that this Python implementation was NOT used to obtain the classification accuracies. The running times are averaged over three runs. Due to limited time, the three runs were run roughly concurrently on our PC.

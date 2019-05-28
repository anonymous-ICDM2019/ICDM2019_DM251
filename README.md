# Note to reviewers

This repository holds the source code and raw experimental results of ICDM 2019 paper DM251. This repository is for reviewing purposes only. All identity information of the authors has been hidden.

# How to use the code

The source code implements both our HBOP algorithm and the BOPF algorithm proposed in 

    Xiaosheng Li, Jessica Lin: Linear Time Complexity Time Series Classification with Bag-of-Pattern-Features. ICDM 2017: 277-286

HBOP.py implements the HBOP algorithm and all its variants (see the "Impact of Design Choices" section in our paper). Note that only the full version of HBOP is timed. BOPF.py implements the BOPF algorithm.

To use the code, please keep all the packages and files in this repository in a single folder. To run HBOP.py, first change the path in line 18 of HBOP.py to your repository path. Then, run the following command in your command council.

    python.exe [full path of HBOP.py] [dataset name] [runId] [mother path of the UCR dataset] [full path of the folder to save the results]

Similarly, to run BOPF.py, first change the path in line 13 of BOPF.py to your repository path. Then, run the following command in your command council.

    python.exe [full path of BOPF.py] [dataset name] [runId] [mother path of the UCR dataset] [full path of the folder to save the results]


# How did we preprocess the data?

We have used datasets from the latest version of the UCR archive 

    Hoang Anh Dau, Eamonn Keogh, Kaveh Kamgar, Chin-Chia Michael Yeh, Yan Zhu, Shaghayegh Gharghabi , Chotirat Ann Ratanamahatana, Yanping Chen, Bing Hu, Nurjahan Begum, Anthony Bagnall , Abdullah Mueen and Gustavo Batista (2018). The UCR Time Series Classification Archive. URL https://www.cs.ucr.edu/~eamonn/time_series_data_2018/
    
For datasets with missing values, we followed the briefing document of the UCR archive, and filled the missing values with linear interpolation. For datasets with variable time series lengths, both HBOP and BOPF can in theory handle such cases directly. However, the original C++ implementation of BOPF demands the time series to be of the same length, thus we opt to conduct this procedure. The UCR  briefing document suggests pedding with low amplitude random values. Instead, we choose to pad zeros. The reason why we make this choice is that the low amplitude values can be significantly amplified after z-normalization. For subsequence-based methods such as BOPF and our HBOP, this may significantly affect the results.

# How did we obtain the experimental results?

In our paper, we compared our HBOP method with three 1NN algorithms and BOPF. The classification error rates of the 1NN algorithms were drawn from the UCR archive webpage. For BOPF, we ran both our Python implementation and the original C++ implementation, and chose the better result. All error rates were rounded to the nearest four decimal digits for comparison.

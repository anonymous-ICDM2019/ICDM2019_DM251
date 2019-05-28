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



# How did we obtain the experimental results?


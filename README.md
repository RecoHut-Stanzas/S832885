# HierarchicyBandit   

## Introduction  
This is the implementation of WSDM 2022 paper : [Show Me the Whole World: Towards Entire Item Space Exploration for Interactive Personalized Recommendations](https://arxiv.org/abs/2110.09905)  
The reference codes for **HCB** and **pHCB**, which are based on three different base bandit algorithms. 
1. LinUCB from [A contextual-bandit approach to personalized news article recommendation](https://dl.acm.org/doi/10.1145/1772690.1772758)  
2. epsilon-Greedy [This strategy, with random exploration on an  epsilon fraction of the traffic and greedy exploitation on the rest]
3. Thompson Sampling from [Thompson Sampling for Contextual Bandits with Linear Payoffs
](http://proceedings.mlr.press/v28/agrawal13.pdf)  

## Files in the folder

- `data/`
  - `MIND/` and `TaoBao/`
     - `item_info.pkl`: processed item file, including item id, item feature and embeddings for simulator;
     - `user_info.pkl`: processed user file, including user id, and embeddings for simulator;
     - `item_info_ts.pkl`:  processed item file for Thompson sampling;
- `algs/`: implementations of PCB and pHCB based on LinUCB.
- `algsE/`:  implementations of PCB and pHCB based on epsilon-Greedy.
- `algsTS/`:  implementations of PCB and pHCB based on Thompson Sampling.   

**Note**
1. Before testing the algorithms, you should modify the settings in config.py. 
2. For thompson sampling, we provide another 16 dimensonal feature vectors to run the experiments, since it can be faster . The original feature vectors are also work with the algorithms.
3. the user_info.pkl and item_info.pkl is formated as dictionary type. 
4. The implementation of ConUCB is released at [ConUCB](https://github.com/Xiaoyinggit/ConUCB). HMAB and ICTRUCB are specical case of CB-Category and CB-Leaf.
5. Datasets can be downloads from : [MIND](https://drive.google.com/file/d/1CBgLI9qgRaKo6ZpAMq1fc3MPjpQtDdkP/view?usp=sharing) and [TaoBao](https://drive.google.com/file/d/1uWPBIHl_dkr089kCwrn0kWXFLxBR88ek/view?usp=sharing)

## Usage:  
Download the HierarchicyBandit.zip and unzip.  You will get five folders, they are `algs/`, `algsE/`, `algsTS/`, `data/`, and `logger/`.   

**Parameters:**  
The config.py file contains:
```
dataset: is the dataset used in the experiment, it can be 'MIND' or 'TaoBao';  
T: the number of rounds of each bandit algorithm;  
k: the number of items recommended to user at each round, default is 1;  
activate_num: the hyper-papamter p for pHCB;  
activate_prob: the hyper-papamter q for pHCB;  
epsilon: the epsilon value for greedy-based algorithms;  
new_tree_file: the tree file name;  
noise_scale: the standard deviation of environmental noise;  
keep_prob: sample ratio; default is 1.0, which means testing all users.
linucb_para: the hyper-parameters for linucb algorithm;
ts_para: the hyper-parameters for thompson sampling algorithm;
poolsize: the size of candidate pool;
random_choice: whether random choice an item to user;   
```   
**Environment:** python 3.6 with Anaconda
**To run the bandit codes based on LinUCB:**  
```
$ cd algs
$ python simulator_multi_process.py
```  
**To run the bandit codes based on epsilon-Greedy:**  
```
$ cd algsE
$ python simulator_multi_process.py
``` 
**To run the bandit codes based on Thompson sampling:**  
```
$ cd algsTS
$ python simulator_multi_process.py
``` 

## Project structure
```
.
├── [ 27K]  algs
│   ├── [2.7K]  clinucb.py
│   ├── [ 970]  config.py
│   ├── [3.3K]  hcb.py
│   ├── [ 865]  item.py
│   ├── [ 944]  logger.py
│   ├── [2.1K]  naive_linucb.py
│   ├── [3.9K]  phcb.py
│   ├── [7.0K]  simulator_multi_process.py
│   └── [ 900]  user.py
├── [ 24K]  algsE
│   ├── [1.7K]  ceg.py
│   ├── [ 954]  config.py
│   ├── [2.8K]  hcb.py
│   ├── [ 865]  item.py
│   ├── [ 944]  logger.py
│   ├── [1.3K]  naive_eg.py
│   ├── [2.7K]  phcb.py
│   ├── [6.9K]  simulator_multi_process.py
│   └── [1.6K]  user.py
├── [ 26K]  algsTS
│   ├── [1.0K]  config.py
│   ├── [2.4K]  cts.py
│   ├── [3.0K]  hcb.py
│   ├── [ 865]  item.py
│   ├── [ 944]  logger.py
│   ├── [1.9K]  naive_ts.py
│   ├── [3.7K]  phcb.py
│   ├── [6.9K]  simulator_multi_process.py
│   └── [1.6K]  user.py
├── [4.3K]  data
│   └── [ 257]  data.txt
├── [427K]  images
│   ├── [118K]  hcb_algo.png
│   ├── [ 63K]  hcb_flow.png
│   ├── [ 79K]  P422159_process_flow.svg
│   ├── [114K]  phcb_algo.png
│   └── [ 49K]  phcb_flow.png
├── [4.0K]  logger
│   └── [  46]  testfile.txt
├── [255K]  nbs
│   └── [251K]  P422159_Entire_item_space_exploration_with_Contextual_bandits_on_MIND_news_dataset.ipynb
├── [3.3K]  README.md
└── [9.8K]  reports
    └── [5.8K]  S832885_report.ipynb

 783K used in 8 directories, 37 files
```

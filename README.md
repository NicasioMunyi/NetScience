# NetScience
### Table of Contents
- [Project Overview](#project-overview)
- [PART 1: Getting Our Project Data Ready](#part-1-getting-our-project-data-ready)
- [PART 2: Graph Representations](#part-2-graph-representations)
- [PART 3: Making Adjustments](#part-3-making-adjustments)
- [PART 4: Degree](#part-4-degree)
- [Conclusion](#conclusion)
### Project Overview

- The project focuses on Facebook connections
- To complete the project, we used existing data "**Facebook Large Page-Page Network Data Set**" from **Kaggle** Database
- The dataset has two columns and 171002 rows
- Nodes represent Official Facebook Pages while the Links/Edges are mutual likes between sites
- Facebook ids with similar likes in Column1 are matched with Facebook ids with similar likes in column 2
- See dataset used on **[Kaggle](https://www.kaggle.com/ishandutta/facebook-large-pagepage-network-data-set)**

### PART 1: Getting Our Project Data Ready
- Our dataset is a comma separated value (csv) file of two columns of facebook ids and connections
- To use the data, we used pandas to read the data as shown below

```py

import pandas as pd
mydata = pd.read_csv(r"D:\KCA\Network Science\Facebook_Network_Edges.csv")
```
- We are interested to show connections between the FaceBook pages and other Pages
- Hence, we need to trim the dataframe into needed columns and store in new dataframe for manipulation
- In this case, from our dataframe above, we have, 'facebook_id_1', 'facebook_id_2'
- We created a new dataframe, so that in case of any changes, the original remains intact

```py

mydata1 = mydata[['Facebook_id_1', 'Facebook_id_2']]
# Overview of the Data Frame
mydata.head

<bound method NDFrame.head of         Facebook_id_1  Facebook_id_2
0                   0          18427
1                   1          21708
2                   1          22208
3                   1          22171
4                   1           6829
...               ...            ...
170997          20188          20188
170998          22340          22383
170999          22348          22348
171000           5563           5563
171001          22425          22425

[171002 rows x 2 columns]>
```

### PART 2: Graph Representations
```py

# First, we created the World into which the Graph will exist
# Here, we needed the NetworkX Python Package, as shown below
# The name of our graph is "GG"
​
import networkx as nx
GG = nx.Graph()

# We can check the Graph for nodes as below
GG.nodes()       # Gives empty since we have not added any Nodes yet
NodeView(())

# We can also check the Graph for edges as below
GG.edges()      # Gives empty since we have not added any edges yet
EdgeView([])
```
- Our dataset is in columns and rows. Next, adding the edges using pandas to created Graph 'GG'
```py
GG = nx.from_pandas_edgelist(mydata1, 'Facebook_id_1', 'Facebook_id_2')

# Next, checking the NEW outlook of the Graph based on Nodes
GG.nodes()

# Next, we can also check the Graph outlook based on Edges
GG.nodes()
```
### Visualizing Graph GG
```py
# Now, we ccneed to visualize the Graph 'GG'
# Here, matplotlib.pyplot Python library was used to make this possible

from matplotlib.pyplot import figure
figure(figsize=(200, 200))                                    # Specifying the figure size
nx.draw_shell(GG,  with_labels=True, node_color='red')
```
- **Below is the Original Dataset's Graph**
![image](https://user-images.githubusercontent.com/77758884/159598159-f483442d-93d7-4ca2-a268-83051cb6491e.png)

### PART 3: Making Adjustments
- As shown above, the created graph using all the collected data is challenging to explain
- To make this simple, we selected only random 200 items from the total 171002 in the original data
```py
import pandas as pd
datafile = pd.read_csv(r"C:\Users\User\Documents\new_data_200_items.csv")
import pandas as pd

# Overview of the dataframe with 15 items
datafile.head(15)


Facebook_id_1	Facebook_id_2
0	32	22467
1	13	22435
2	1	22405
3	6	22403
4	4	22401
5	3	22338
6	32	22330
7	2	22304
8	1	22265
9	6	22261
10	1	22208
11	33	22181
12	26	22177
13	37	22177
14	1	22171
```
- Creating new graph **GS** that will form the world for the connections
​
```py
import networkx as nx
GS = nx.Graph()
GS = nx.from_pandas_edgelist(data500, "Facebook_id_1", "Facebook_id_2")
```
- We can get an overview of the Graph GS, based on Nodes
```py
GS.nodes()

NodeView((
32, 22467, 13, 22435, 1, 22405, 6, 22403, 4, 22401, 3, 22338, 22330, 2, 22304, 22265, 22261, 22208, 33, 22181, 26, 22177, 37, 
22171, 14, 22020, 24, 21955, 27, 21785, 5, 21768, 21755, 21729, 21708, 21631, 31, 21598, 21538, 36, 21489, 12, 21430, 35, 21424,
22, 21325, 21323, 21280, 21247, 38, 21229, 21221, 21157, 17, 21059, 21035, 20983, 18, 20938, 19, 20923, 29, 20895, 20876, 20829,
20655, 20624, 20510, 20435, 20280, 20276, 20271, 20135, 11, 20092, 20071, 20024, 19957, 19901, 19837, 19753, 19743, 19700, 23,
19678, 19643, 19574, 19509, 19489, 19356, 19337, 19252, 19222, 19111, 18949, 18893, 18886, 18858, 18782, 18754, 18727, 18725,
18703, 15, 18689, 7, 18601, 18512, 18497, 18468, 25, 18449, 0, 18427, 28, 18396, 18391, 18374, 18368, 18304, 21, 18272, 18263,
39, 18234, 18217, 18216, 18153, 18062, 18059, 18037, 18024, 17984, 30, 17983, 17866, 17848, 17845, 17833, 17818, 17772, 17728,
17695, 17554, 17507, 17460, 17433, 17411, 17370, 17363, 17354, 17350, 17346, 17325, 17252, 17242, 17178, 17163, 17090, 17088,
17038, 16994, 16972, 16895, 16885, 16854, 16742, 16630, 16615, 16606, 16590, 16534, 16524, 16420, 16417, 16406, 16399, 16282,
16260, 16203, 16128, 16071, 16052, 15868, 15807, 15785, 15735, 15690, 15644, 15531, 15507, 15368, 15359, 15323, 15191, 15174,
15172, 15129, 15026, 14971, 14944, 14862, 14840, 14832, 14791, 14790, 14768, 14666, 34, 14650, 14628, 14597, 14547, 9, 14497,
14467, 14454, 14409, 14392, 14344, 14332, 14248, 14241, 8, 14205, 14179, 14164))
```
- Now, we need to visualize the Graph 'Gs', with the help of **matplotlib.pyplot** Python library
```py
from matplotlib.pyplot import figure
figure(figsize=(100, 100))                                    # Specifying the figure size
nx.draw_shell(GS,  with_labels=True, node_color='red')
```
<div align="center">
  
  ![image](https://user-images.githubusercontent.com/77758884/159599622-70953b15-c52f-4e0c-8470-70524e705a1e.png)
 
</div>

- To get a better view of the connections, we can modify the graph's outlok by choosing the **draw_networkx** option
```py
from matplotlib.pyplot import figure
figure(figsize=(50, 50))                                    # Specifying the figure size
nx.draw_networkx(GS,  with_labels=True, node_color='red')
```
![image](https://user-images.githubusercontent.com/77758884/159599897-b6ca053a-fb78-4fd2-be79-e1969371a16e.png)

### PART 4: Degree
- Next, we also created another dataframe that shows the nodes and their number of connections.
- Using online resources, the following scripts helped depict the nodes and number of connections on each
```py
connectionsBoard = {}
for x in GS.nodes:
    connectionsBoard[x] = len(GS[x])
s = pd.Series(connectionsBoard, name='Connections')
connectionDataframe = s.to_frame().sort_values('Connections', ascending = False)
```
- We can get an overview of the connections as shown below:
```py
connectionDataframe.head(22)

14	18
32	17
1	17
4	14
18	14
26	12
5	12
22	10
37	8
29	8
6	7
19	5
39	5
12	4
3	4
2	4
31	4
38	3
13	3
30	3
28	3
11	2
18024	2

```
- From the information above, person 14 (node 14) has the largest connections[links], and hence highest degree
- This is also evident as shown in the network connection representation/graph above, with a snippet below:

<div align="center"
     
![image](https://user-images.githubusercontent.com/77758884/159600488-8502a97c-8853-4e9c-8ffb-3e2e78f93811.png)
     
</div>

### Conclusion
- Using past **[Data](https://www.kaggle.com/ishandutta/facebook-large-pagepage-network-data-set)**, it was possible to visualize the Facebook connections
- The main **Python** libraries and packages used were **networkx, pandas and matplotlib**
- As shown with the **Facebook** network, people have varying connections with varied degrees based on their links

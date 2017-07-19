#  Predictive tools for Higher Ed cultures that prioritize personal & career development.

## 1. What are we building?

This is the MVP of a platform that will deliver the data on the association of social ties with academic and labor/job outcomes.

What you will be building is the social graph of a freshman college class. This exercise is meant to build the shell of the graph, where the 475 students of a freshman class are tied by class associations. What we will be measuring includes:

#### Degree centrality — the number of social ties a node has in a social network
#### Closeness centrality — the distance of a node to all other nodes in a social network
#### Betweenness centrality —the number of shortest paths between any two nodes that go through a given node
#### Eccentricity—the distance between a node and its farthest node in a socialnetwork

Details of the files are given below.

## 2. What stack are we using?

#### Database: SQL
#### Backend: Django
#### Frontend: React & Redux

## 3. What are the files provided?
The files provided are all in JSON format.

### freshmanclass.json
This file provides genereal information on the freshman class. The `credits` indicates the number of credit hours taken. The `DOB` is the birth year for age. `First Gen` indicates whether the student is a first generation college student. `GPA` is the current cumulative GPA. `Home` is the hometown information including a zip code, Town and State. The `Transcript` is the set of courses a student is taking. `Gender` is as given and `index` is a unique identifier.


```json
{
    "CLASS2021": [
        {
            "Credits": 16, 
            "DOB": 1999, 
            "First Gen": "yes", 
            "GPA": 2.24, 
            "Home": [
                "14822", 
                "Canaseraga", 
                "NY"
            ], 
            "Transcript": [
                "CRE 119", 
                "THE 141", 
                "BOT 115", 
                "AMS 102"
            ], 
            "gender": "male", 
            "index": "de77d26f-4048-47f9-a8c8-ee2f70612761"
        }, 
```
### freshmenmapping.json
This file provides you with the data fro essentially a 475 x 475 matrix that provides you with the degree closeness of each freshman in the class. The example below shows that `de77d26f-4048-47f9-a8c8-ee2f70612761` isn't connected to `b463f794-b2d4-4092-a6b1-94c4d5341def` but is `2` times connected to `25b89d42-d83d-41f6-b3e5-110a31e38ae8`.
```json
{
        "mapping": [
            "de77d26f-4048-47f9-a8c8-ee2f70612761", 
            "b463f794-b2d4-4092-a6b1-94c4d5341def"
        ], 
        "value": 0
    },
{
        "mapping": [
            "de77d26f-4048-47f9-a8c8-ee2f70612761", 
            "25b89d42-d83d-41f6-b3e5-110a31e38ae8"
        ], 
        "value": 2
    }, 


```
#### HINT: to quickly access this matrix values, you can use `freshmanclass.json` and extract all the index keys and then iterate through the `freshmenmapping.json` file.

### LaplacianCentrality.json
This file provides you with the calculated laplacian values of each node and its corresponding Laplacian Value
```json
{
        "centrality": 0.004371616654982276, 
        "node": "c7f15085-1089-4fbd-9c19-8c26e22fa279"
    },
```

### BetweennessCentralityMatrix.json
This file represents the extent to which a student lies on paths between other students. Students with high betweenness may have considerable influence within the network by virtue of their control over information passing between others. They are also the ones whose removal from the network will most disrupt communications between other vertices because they lie on the largest number of paths taken by messages. Each betweenness is affiliated with a unique id `"0264e0f5-f9aa-4a39-865b-32911eeb0185": 183.16906392420418`

### ClosenessCentralityMatrix.json
Closeness centrality of a student is the reciprocal of the sum of the shortest path distances from one student to all other students. The higher the value, the more central the student is. 

### DegreeCentralityMatrix.json
The degree centrality for a student is the fraction of student he / she is connected to. The higher, the more exposed the student is to the network. For example, this is a 9% and 13% connection respectively:
```json
"f01db5a5-abcf-402b-ba9f-b964dfa869a0": 0.09915611814345991, 
"f144b744-1184-4917-b859-debc3d9935f7": 0.13080168776371306, 
```

### EccentricityMatrix.json
The eccentricity of a student is the maximum distance from the student to all other students.

## 4. The Task

### 1. UI / UX
Design-wise, feel free to use any source that is licensed / open source. The color scheme to keep in mind is as follows: `E61B59` and `86C5E5` in addition to black and white. Font choice is `Brandon Text` and `Brandon Grotesque`.
Logos are attached as `Logo_Black.jpg` and `Logo_White.jpg`

### 2. PERMISSIONS / VIEWS

#### 2A. Private Side
The private side should be able to display all the student-related data. That is their biodata, as well as clustering around their various centralities (feel free to commit to up to 4 buckets when you do any clustering). You should display the various centralities on different tabs / cards with the following naming: 'THE BETWEENERS', 'THE CLOSENESS', 'THE CENTRALISTS', 'THE REMOVED'.
For ideas on how to show clustering, please see the following:
##### [https://bost.ocks.org/mike/miserables/] (Adjacency Matrix)
##### [http://amp.pharm.mssm.edu/clustergrammer/viz_sim_mats/58a492b4a63cb826f0be6476/rc_two_cats.txt] (Clustergrammer)

#### 2B. Public Side
Stick to the adjacency matrix model. The value you measure shoudl be based on the number of shared courses but anonymize the students. (The file to look at is the `freshmanmapping.json`) Look to sort the students by 1) `Centrality measures` 2) `GPA` 3) `AGE` 4) `NUMBER OF COURSES`

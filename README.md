# AI-Project-SearchAlgos
Hey... 
This repository have been created for those who are curious about how search algorithms work!

* the executable application for windows, linux, macintosh, android and ios will be ready soon and will be shared here.
* the webpage for project is [here](https://tan-paralleluniverse.github.io/ai-project-searchalgos/)

#### some features of the complete application will contain:
```
* user can choose the search algorithm and map for visualizing search algorithms
for better understanding of updating loops and time order of each algorithm.

* there is 7 maps right now inside the existing project that can be accessed from
asset folder and they will be default maps inside the completed application.

* user can draw arbitrary maps in photoshop and each pixel will be interpreted
as a node in graph.

* user can choose starting and ending point for search algorithms
```
# Getting Started
repository is a whole Unity Project so that contains many assets.
All the codes are stored in "/assets/scripts" folder and written in C# (but the logic is understandable so stop freaking out!).
For the sake of easiness I have seperated the algorithms from "Pathfinder" class and attached them in README file.
The whole Project is based on object oriented programming concept so following the code is not that hard, just a little search for methods will bring you to the class that contains it.
# Stucture of scripts
Well, 

Inside the "scrips" folder there are several classes :

- Scripts
  - [ ] DemoController.cs
  - [ ] Graph.cs
  - [ ] GraphView.cs
  - [ ] MapData.cs
  - [ ] Node.cs
  - [ ] NodeView.cs
  - [x] Pathfinder.cs
  - [ ] PriorityQueue.cs
  
  BUT for now, the documentation aims to focus on algorithmes and less dedicate efforts to other aspects like how we model the graph or how we create map and connect nodes in map as we connect nodes in graph and tadadada ... 
	
## BFS Algorithm : Class ExpandFrontierBreadthFirst
```
void ExpandFrontierBreadthFirst(Node node)
    {
        if (node != null)
        {
            for (int i = 0; i < node.neighbors.Count; i++)
            {
                if (!m_exploredNodes.Contains(node.neighbors[i])
                    && !m_frontierNodes.Contains(node.neighbors[i]))
                {
                    float distanceToNeighbor = m_graph.GetNodeDistance(node, node.neighbors[i]);
                    float newDistanceTraveled = distanceToNeighbor + node.distanceTraveled
                                                                         + (int)node.nodeType;
                    node.neighbors[i].distanceTraveled = newDistanceTraveled;

                    node.neighbors[i].previous = node;
                    node.neighbors[i].priority = m_exploredNodes.Count;

                    m_frontierNodes.Enqueue(node.neighbors[i]);
                }
            }
        }
    }
```
## Dijkastra Algorithm : Class ExpandFrontierDijkstra

```
void ExpandFrontierDijkstra(Node node)
    {
        if (node != null)
        {
            for (int i = 0; i < node.neighbors.Count; i++)
            {
                if (!m_exploredNodes.Contains(node.neighbors[i]))
                {
                    float distanceToNeighbor = m_graph.GetNodeDistance(node, node.neighbors[i]);
                    float newDistanceTraveled = distanceToNeighbor + node.distanceTraveled
                                                                         + (int)node.nodeType;

                    if (float.IsPositiveInfinity(node.neighbors[i].distanceTraveled) ||
                        newDistanceTraveled < node.neighbors[i].distanceTraveled)
                    {
                        node.neighbors[i].previous = node;
                        node.neighbors[i].distanceTraveled = newDistanceTraveled;
                    }

                    if (!m_frontierNodes.Contains(node.neighbors[i]))
                    {
                        node.neighbors[i].priority = (int)node.neighbors[i].distanceTraveled;
                        m_frontierNodes.Enqueue(node.neighbors[i]);
                    }
                }
            }
        }
    }
```
## GreedyBFS Algorithm : Class ExpandFrontierGreedyBestFirst
```
void ExpandFrontierGreedyBestFirst(Node node)
    {
        if (node != null)
	{
	    for (int i = 0; i < node.neighbors.Count; i++)
	    {
		if (!m_exploredNodes.Contains(node.neighbors[i])
		    && !m_frontierNodes.Contains(node.neighbors[i]))
		{
		    float distanceToNeighbor = m_graph.GetNodeDistance(node, node.neighbors[i]);
		    float newDistanceTraveled = distanceToNeighbor + node.distanceTraveled
									 + (int)node.nodeType;
		    node.neighbors[i].distanceTraveled = newDistanceTraveled;
		    node.neighbors[i].previous = node;
                    if (m_graph != null)
                    {
                        node.neighbors[i].priority = (int)m_graph.GetNodeDistance(
                            node.neighbors[i], m_goalNode);
                    }
					

		    m_frontierNodes.Enqueue(node.neighbors[i]);
		}
	    }
	}
    }
```
## A* Algorithm : Class ExpandFrontierAStar
```
void ExpandFrontierAStar(Node node)
    {
	if (node != null)
	{
	    for (int i = 0; i < node.neighbors.Count; i++)
	    {
		if (!m_exploredNodes.Contains(node.neighbors[i]))
		{
		    float distanceToNeighbor = m_graph.GetNodeDistance(node, node.neighbors[i]);
		    float newDistanceTraveled = distanceToNeighbor + node.distanceTraveled
									+ (int)node.nodeType;

		     if (float.IsPositiveInfinity(node.neighbors[i].distanceTraveled) ||
			newDistanceTraveled < node.neighbors[i].distanceTraveled)
		    {
			node.neighbors[i].previous = node;
			node.neighbors[i].distanceTraveled = newDistanceTraveled;
		    }

                    if (!m_frontierNodes.Contains(node.neighbors[i]) && m_graph != null)
		    {
                        int distanceToGoal = (int)m_graph.GetNodeDistance(node.neighbors[i], m_goalNode);
                        node.neighbors[i].priority = (int)node.neighbors[i].distanceTraveled 
                            + distanceToGoal;
			m_frontierNodes.Enqueue(node.neighbors[i]);
		    }
		}
	    }
	}
    }
```
## Deployment

[Unity game engine](https://unity3d.com/get-unity/download) has to be installed on the device and the whole repository has to be added as a new project.


## Built With

* [Unity game engine](https://unity3d.com/get-unity/download) - The game engine VERSION 2018.1.6F1
* [photoshop](https://www.adobe.com/se/products/photoshop.html?gclid=EAIaIQobChMImM-miafD3wIVFKaaCh3r9gboEAAYASAAEgJEwvD_BwE&sdid=8JD95K3M&mv=search&ef_id=EAIaIQobChMImM-miafD3wIVFKaaCh3r9gboEAAYASAAEgJEwvD_BwE:G:s&s_kwcid=AL!3085!3!281083711561!e!!g!!adobe%20photoshop) - Map Generation
* [Microsoft Visual Studio](https://visualstudio.microsoft.com/) - Used as IDE instead of [monodevelop](https://www.monodevelop.com/) with all respect :D
## Versioning

I use [Git](https://git-scm.com/downloads) for versioning. For the versions available, see the [tags on this repository](https://github.com/ai-project-searchalgos/ai-project-searchalgos/tags). 
## Authors

* **Amir Hossein Dezhbro** - *Initial work* - [tan-ParallelUniverse](https://github.com/tan-ParallelUniverse/graphs/contributors)

See also the list of [contributors](https://github.com/tan-ParallelUniverse/ai-project-searchalgos) who participated in this project.
## License
This project is licensed under the MIT License - see the [LICENSE](https://github.com/tan-ParallelUniverse/LICENSE) file for details
## Acknowledgments
* the credit of this project (if there is any credit :D) goes to the ai class under supervision of prof.ghazanfari and dr.ghiasi.
* the executable application for windows, linux, macintosh, android and ios will be ready soon and will be shared here.
#### * feel free to contact for contribution or fork the project, im open to new ideas and contributions. more algorithms need to be added and I have not enough time to add them but since the whole code is object oriented you can add more algorithms and make the application more perceiving on algorithms.


# AI-Project-SearchAlgos
Hey... 
This repository have been created for those who are curious about how search algorithms work!
## Getting Started
repository is a whole Unity Project so that contains many assets.
All the codes are stored in "/assets/scripts" folder.
For the sake of easiness I have seperated the algorithms from "Pathfinder" class and attached them in README file.
The whole Project is based on object oriented programming concept so following the code is not that hard, just a little search for methods brings you to the class that contains it.
## BFS Algorithm : Class ExpandFrontierBreadthFirst
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
## Dijkastra Algorithm : Class ExpandFrontierDijkstra
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

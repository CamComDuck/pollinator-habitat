---
title: Pollinator Habitat Project
---
classDiagram
    class Player{
        -int visitId
        +int routesCompleted

        +advance(nodeId)
        +finishRoute(routeId)
        +quickRestart(visitId, routesCompleted) 
        +setRoutePreferences()
        +setAccessibilityFeatures()
    }

    class Node{
        -int nodeId
        -String nodeInfo
        -bool endOfRoute
        +List connectedNodes
        +getNodeInfo(nodeId)
    }
    class endNode{
        -int nodeId
        -String nodeInfo
        -bool endOfRoute
        +List connectedNodes
        -String pollinatorFacts
        +getFactSheet(nodeId)
    }

    class Route{
        -int routeId
        +List routeNodes
    }

Node --> Node : player moves from
Route o-- Node : connects
Player --> Route : follows
FinalNode --|> Node : is a
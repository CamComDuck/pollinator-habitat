---
title: Pollinator Habitat Project
---
classDiagram
    class player{
        -int visitId
        +int routesCompleted

        +advance(nodeId)
        +finishRoute(routeId)
        +quickRestart(visitId, routesCompleted) 
        +setRoutePreferences()
    }

    class node{
        -int nodeId
        -String nodeInfo
        -bool endOfRoute
        +List connectedNodes
    }

    class route{
        -int routeId
        +List routeNodes
    }

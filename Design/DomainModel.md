---
title: Pollinator Habitat Project
---
classDiagram

    class Node{
        -nodeId: int
        -nodeInfo: String
        -endOfRoute: bool
        +connectedNodes: List<Node>
        +getNodeInfo(nodeId): String
    }
    class FinalNode{
        -nodeId: int
        -nodeInfo: String
        -endOfRoute: bool
        +connectedNodes: List<Node>
        -pollinatorFacts: String
        +getFactSheet(nodeId): String
    }

    class Route{
        -routeId: int
        +routeNodes: List<Node>
    }
     class Player{
        -playerId: int 
        +routesCompleted: List<Route>
        +advance(nodeId) : Node
        +finishRoute(routeId) : void
        +quickRestart(visitId, routesCompleted) : Node
        +setAccessibilityFeatures() : void
    }
    class Session{
        -sessionId: int
        -players: List<Player>
        -routes: List<Route>
    }

Node --> Node : player moves from
Route o-- Node : connects
Player --> Route : follows
FinalNode --|> Node : is a
Session o-- Route : establishes
Session o-- Player : participates in
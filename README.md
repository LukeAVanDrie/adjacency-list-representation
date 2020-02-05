## Artifact 2: Representing a Graph as an Adjacency List

### Creating the Adjacency List (using JavaScript ES6):

1. Determine a representation for a vertex (node) that contains a list of edges.

   * What additional information does your vertex need to contain (name, order created, id, etc.)? 

     ```javascript
     // this is a factory function that will serve as a constructor for new vertices
     const CreateVertex = (name, id, edges = []) => {
         name: name,
         id: id,
         edges: edges
     }
     ```

2. Determine a representation for an edge.

   * Other than the destination node, do you need additional information such as weights?

     ```javascript
     // this is a factory function that will serve as a constructor for new edges
     const CreateEdge = (destination, weight = 1) => {
         destination: destination,
         weight: weight
     }
     ```

3. Create a list structure to store your vertices. Since edges are properties of a vertex, they can be added to the elements of the list later.

   ```javascript
   let v1 = CreateVertex("Vertex 1", 1);
   let v2 = CreateVertex("Vertex 2", 2);
   let graph = [v1, v2];
   graph[0].edges.push(createEdge(graph[1], 0.7));
   ```
   
   * For undirected edges between v1 and v2, add an edge with destination = v2 to v1 and an edge with destination = v1 to v2. Ensure that they have the same or no weights.

     ```javascript
  let graph = [v1, v2];
     graph[0].edges.push(createEdge(graph[1], 0.5));
     graph[1].edges.push(createEdge(graph[0], 0.5));
     ```

   * It may be helpful to create a helper function for adding undirected edges that abstracts this work.

     ```javascript
     const CreateUndirectedEdge = (v1, v2, weight = 1) => {
         v1.edges.push(createEdge(v2, weight));
         v2.edges.push(createEdge(v1, weight));
     }
     
     let graph = [v1, v2];
     CreateUnidrectedEdge(graph[0], graph[1], 0.6);
     ```

**Alternative Approach:** 

An alternative approach to creating an adjacency list is representing your graph as an object where the vertex ids are the keys and a list of edges are the values. In this case, the edge object must be modified to also contain a source vertex to properly link the objects. This is more reminiscent of a relational structure between the vertex objects than the provided approach which actually links the neighboring vertices as a property of the vertex object; however, it is more similar to the map/dictionary approach for adjacency lists that is commonly used.  

### Accessing the Vertices from the Adjacency List:

* Getting a vertex: a vertex is an element of the adjacency list.

  ```javascript
  let graph = [v1, v2, v3, v4, v5];
  let desiredVertex = graph[3] // when accessing v4
  ```

* Getting all neighboring vertices from a particular vertex: the neighbors are the destination vertices of the edges of a particular vertex.

  ```javascript
  let graph = [v1, v2, v3, v4, v5];
  let desiredVertex = graph[3];
  
  // get the edges with their associated properties
  let edges = desiredVertex.edges;
  
  // get just the neighboring vertices
  let neighbors = edges.map((edge) => {
  	return edge.destination;
  });
  ```

### Should I Use an Adjacency List?

**Pros:**

- An adjacency list is fairly simple to implement.
- Getting the neighboring vertices or edges for a particular vertex is very easy.
- It allows for additional properties to be associated with vertices and edges unlike the adjacency matrix.

**Cons:**

- While our approach using an array of vertex objects with a property containing a list of edges allows for the graph representation to be ordered, the alternate and more common approach using a map is not guaranteed to retain order.
- The data structure we build to hold our adjacency list has a lot more overhead than using other representation approaches such as the adjacency matrix or bag of edges.
- To find a particular neighbor or edge, one must perform a linear search on the array of edges stored on a particular vertex.
- It lacks the visual simplicity of an adjacency matrix which facilitates ease of identifying edges between vertices.

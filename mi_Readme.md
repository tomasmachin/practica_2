# Inteligencia Artificial

## Práctica 3: Búsqueda heurística. 
___
## Pasos a realizar:

1. Hacer un git clone del proyecto: `git clone https://github.com/phishman3579/java-\algorithms-implementation.git`
2. Examinar el código del método de `aStar` de la clase `AStar.java` y posteriormente los tests localizados en: [java-algorithms-implementation/test/com/jwetherell/algorithms/graph/test/Graphs.java]()
3. Después desarrolle un código de prueba:

    ~~~javascript
    package aplicacion;
    
    public class Main{
            public static void main(String[] args){
                System.out.println("Esto es una prueba");
            }
    }
    ~~~
   
4. Posteriormente añadir/sustituir al archivo `build.xml` las siguientes líneas:
   - Añadir el siguiente código en la zona indicada por: `<!– set global properties for this build –>`
   ~~~html
     <property name="main-class" value="aplicacion.Main"/>
   ~~~
   - El `target` de `dist` se debe modificar de la siguiente manera:
   ~~~html
     <target name="dist" depends="build" description="generate thedistribution">
         <jar jarfile="${dist}/java-algorithms-implementation-${DSTAMP}.jar"basedir="${build}">
             <manifest>
                 <attribute name="Main-Class" value="${main-class}"/>
             </manifest>
         </jar>
     </target>
   ~~~
   - Luego añadimos:
   ~~~html
     <target name="run_main" depends="dist">
         <java jar="${dist}/java-algorithms-implementation-${DSTAMP}.jar"fork="true"/>
     </target>
   ~~~
   - Finalmente comprobamos que todo funcione correctamente ejecutando el comando: `ant run_main`
   

5. Una vez realizada la comprobación, se debe crear un programa más desarrollado que genere un camino 
     aplicando A*.

   ~~~javascript
   package aplicacion;
   
   import static org.junit.Assert.assertFalse;
   import static org.junit.Assert.assertTrue;
   
   import java.util.ArrayList;
   import java.util.HashMap;
   import java.util.Iterator;
   import java.util.List;
   import java.util.Map;
   
   import com.jwetherell.algorithms.graph.AStar;
   
   import com.jwetherell.algorithms.data_structures.Graph;
   import com.jwetherell.algorithms.data_structures.Graph.Edge;
   import com.jwetherell.algorithms.data_structures.Graph.TYPE;
   import com.jwetherell.algorithms.data_structures.Graph.Vertex;

   public class Main{
       public static void main(String[] args){
           DirectedGraph directedGraph = new DirectedGraph();
           AStar aEstrella = new AStar();
         
           System.out.println(aEstrella.aStar(directedGraph.graph, directedGraph.v1, directedGraph.v5));
       }
     // Directed
     private static class DirectedGraph {
         final List<Vertex<Integer>> verticies = new ArrayList<Vertex<Integer>>();
         final Graph.Vertex<Integer> v1 = new Graph.Vertex<Integer>(1);
         final Graph.Vertex<Integer> v2 = new Graph.Vertex<Integer>(2);
         final Graph.Vertex<Integer> v3 = new Graph.Vertex<Integer>(3);
         final Graph.Vertex<Integer> v4 = new Graph.Vertex<Integer>(4);
         final Graph.Vertex<Integer> v5 = new Graph.Vertex<Integer>(5);
         final Graph.Vertex<Integer> v6 = new Graph.Vertex<Integer>(6);
         final Graph.Vertex<Integer> v7 = new Graph.Vertex<Integer>(7);
         final Graph.Vertex<Integer> v8 = new Graph.Vertex<Integer>(8);
         {
             verticies.add(v1);
             verticies.add(v2);
             verticies.add(v3);
             verticies.add(v4);
             verticies.add(v5);
             verticies.add(v6);
             verticies.add(v7);
             verticies.add(v8);
         }
         final List<Edge<Integer>> edges = new ArrayList<Edge<Integer>>();
         final Graph.Edge<Integer> e1_2 = new Graph.Edge<Integer>(7, v1, v2);
         final Graph.Edge<Integer> e1_3 = new Graph.Edge<Integer>(9, v1, v3);
         final Graph.Edge<Integer> e1_6 = new Graph.Edge<Integer>(14, v1, v6);
         final Graph.Edge<Integer> e2_3 = new Graph.Edge<Integer>(10, v2, v3);
         final Graph.Edge<Integer> e2_4 = new Graph.Edge<Integer>(15, v2, v4);
         final Graph.Edge<Integer> e3_4 = new Graph.Edge<Integer>(11, v3, v4);
         final Graph.Edge<Integer> e3_6 = new Graph.Edge<Integer>(2, v3, v6);
         final Graph.Edge<Integer> e6_5 = new Graph.Edge<Integer>(9, v6, v5);
         final Graph.Edge<Integer> e6_8 = new Graph.Edge<Integer>(14, v6, v8);
         final Graph.Edge<Integer> e4_5 = new Graph.Edge<Integer>(6, v4, v5);
         final Graph.Edge<Integer> e4_7 = new Graph.Edge<Integer>(16, v4, v7);
         final Graph.Edge<Integer> e1_8 = new Graph.Edge<Integer>(30, v1, v8);
         {
             edges.add(e1_2);
             edges.add(e1_3);
             edges.add(e1_6);
             edges.add(e2_3);
             edges.add(e2_4);
             edges.add(e3_4);
             edges.add(e3_6);
             edges.add(e6_5);
             edges.add(e6_8);
             edges.add(e4_5);
             edges.add(e4_7);
             edges.add(e1_8);
         }
         final Graph<Integer> graph = new Graph<Integer>(Graph.TYPE.DIRECTED, verticies, edges);
     }
   }
   ~~~

6. Como último paso a entregar la práctica, se contestan una serie de preguntas:
   1. **¿Qué variable representa la lista ABIERTA?**
   > La variable que representa la lista abierta del algoritmo **A***, del código proporcionado es la variable **openset**.   
   > Esta variable representa el nodo que va a ser evaluado en ese momento.
   2. **¿Qué variable representa la función g?**
   > La variable que representa la lista abierta del algoritmo **A***, del código proporcionado es la variable **gScore**.  
   > Esta variable representa el coste total del mejor camino conocido hasta el momento, desde inicio al destino.
   3. **¿Qué variable representa la función f ?**
   > La variable que representa la lista abierta del algoritmo A*, del código proporcionado es la variable **fScore**.  
   > Esta variable representa el coste del camino desde el inicio pasando por un nodo en concreto. 
   4. **¿Qué método habría que modificar para que la heurística representara la distancia aérea entre vértices?**
   > El método a modificar sería:
   >~~~javascript
   >   protected int heuristicCostEstimate(Graph.Vertex<T> start, Graph.Vertex<T> goal) {
   >     return 1;
   > }
   >~~~ 
   5. **¿Realiza este método reevaluación de nudos cuando se encuentra una nueva ruta a un determinado vértice? Justifique la respuesta**
   > Si se realiza una reevaluación. Esta sucede en el método:
   > ~~~javascript
   > private List<Graph.Edge<T>> reconstructPath(Map<Graph.Vertex<T>,Graph.Vertex<T>> cameFrom, Graph.Vertex<T> current) {
   >     final List<Graph.Edge<T>> totalPath = new ArrayList<Graph.Edge<T>>();
   >     while (current != null) {
   >         final Graph.Vertex<T> previous = current;
   >         current = cameFrom.get(current);
   >         if (current != null) {
   >             final Graph.Edge<T> edge = current.getEdge(previous);
   >             totalPath.add(edge);
   >         }
   >     }
   >     Collections.reverse(totalPath);
   >     return totalPath;
   > }
   > ~~~
   > Este método se encarga de crear el camino ideal que se debe recorrer para llegar al nodo final, para ello va comprobando 
   > los nodos anteriores hasta el inicial y asi construir el camino mas corto.

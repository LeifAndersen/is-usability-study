You are designing a global shipping network that connects cities together
through a number of shipping lanes. Each shipping lane is a direct path between
two cities, and has a cost to operate. One city is connected to another if their
is a sequence of shipping lanes that connects the two cities. You need to ensure
that for each city, there is a route that connects it to every other city.
However, to save operating costs, you also need to ensure that there is no more
than one route connecting any two cities together.

So for example, the following is city network is valid (slid lines indicate
selected routes between cities):

<p align="center">
<img src="./questions/mst/valid.svg" alt="Display Diagram" 
     style="width:15em;max-width:100%"></p>

However, these network are not valid. The left network has multiple routes from
Paris to Vancouver, and the right network separates New York and Paris from the
rest of the network:

<p align="center">
<img src="./questions/mst/invalid1.svg" alt="Display Diagram" 
     style="width:15em;max-width:100%;margin-right:5em;">
<img src="./questions/mst/invalid2.svg" alt="Display Diagram" 
     style="width:15em;max-width:100%"></p>

Since some connections are more expensive to travel than others. So while still
ensuring that no more than one route exists between any two cities, you want to
find the least expensive network to operate.

For this simple network of Paris, Cairo, and New York, its cheapest to have a
shipping lane from New York to Cairo and New York to Paris. Note that there is
no direct route connecting Cairo to Paris.

<p align="center">
<img src="./questions/mst/cheap.svg" alt="Display Diagram" 
     style="width:15em;max-width:100%"></p>

The group of all cities and possible shipping lanes is represented as a set of
routes, with cities represented as strings and prices as integers. The map above is:

```clojurescript
#{["New York" "Paris" 5]
  ["New York" "Cairo" 10]
  ["Paris" "Cairo" 15]}
```

The resulting network is a subset of this space:

```clojurescript
#{["New York" "Paris" 5]
  ["New York" "Cairo" 10]}
```

Both the group of cities and the network can be described as:

```clojurescript
(s/def ::route (s/cat :from string? :to string? :cost integer?))
(s/def ::cities (s/* ::route))
(s/def ::network (s/* ::route))
```

Finally, three functions help solve this task. First, `connected?` determines if
two cities are connected in a given network. Second, `cheapest-route` finds the
cheapest, valid, route in a group of cities and routes. Finally,
`valid-network?` takes a network, and determines if the network is valid. These
functions meet the following spec:

```clojurescript
(s/fdef connected?
  :args (s/cat :network ::network :start ::route :end ::route)
  :ret boolean?)
(s/fdef cheapest-route
  :args (s/cat :acc ::network :in ::cities)
  :ret ::route
  :fn #(contains? (-> % :args :in) (:ret %)))
(s/fdef valid-network?
  :args (s/cat :in ::network)
  :ret boolean?)
```


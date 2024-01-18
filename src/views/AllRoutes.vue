<template>

<div>
  
  <h3> All Route  </h3>
  
  <div class="container">

<!-- Task 1 -->
<table>
          <tr>
            <th>From</th>
            <th>To</th>
            <th>Cost</th>
            <th>Time</th>
            <th>Date</th>
          </tr>


          <tr class="item" v-for="route in routes" :key="route.code">
          <td>{{ route.fromcity }}</td>
          <td>{{ route.tocity }}</td>

          <td class='red' v-if="route.cost > 12">{{ route.cost }}</td>
          <td class='blue' v-else>{{ route.cost }}</td>
          
          <td>{{ route.departuretime}} </td>
          <td>{{ route.departuredate}} </td>

          </tr>


</table>




</div>

<p class="total-trips"> We have {{ tripsCount }} trips today!</p>

</div>




</template>



<script>
export default {
  name: "AllRoutes",
  data() {
    return {
      toTallinn: 0,
      routes: [],

    };
  },

  computed:{

    tripsCount(){
      return this.routes.length
    }

  },


  methods: {
    fetchRouts() {
      fetch(`http://localhost:3000/api/routes/`)
        .then((response) => response.json())
        .then((data) => (this.routes = data))
        .catch((err) => console.log(err.message));
   },

  },
  mounted() {
    this.fetchRouts();
    console.log("mounted");
  } 
};
</script>





<style scoped>

/* Task 2 */

th {
  background: rgb(111, 142, 105)
}

td {
  background: lightgreen;
}

th, td {
  font-size: 16px;
  margin-bottom: 5px;
  padding: 8px 10px;
}

.container {
  display: flex;
  justify-content: center;
  margin: auto;
  margin-top: 130px;
  width: 25%;
  padding: 20px 10px;
  background-color: lightgray;
}

.blue{
  background-color: lightblue;

}

.red{
  background-color: red;

}

.total-trips{
  display: flex;
  justify-content: center;
  margin: auto;
  width: 25%;
  padding: 20px 10px;
  background-color: gray;

}


</style>
<script>
    import Scatterplot from "../../04_practical/01_custom_components/components/Scatterplot.svelte";
    let datapoints_from_app = [];
    fetch("https://vda-lab.gitlab.io/datavis-technologies/assets/flights_part.json")
        .then(res => res.json())
        .then(data => datapoints_from_app = data)

  </script>
  
<h1>Airports</h1>
<Scatterplot datapoints = {datapoints_from_app} />
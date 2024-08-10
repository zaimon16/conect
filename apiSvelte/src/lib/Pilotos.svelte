<script>
  export let driver;
</script>

<div id="piloto">
  <img id="imgpiloto" src={driver.headshot_url} alt="Img piloto" />
  <h3>Nombre: {driver.full_name}</h3>
  <h4>Scuderia: {driver.team_name}</h4>
  <h4>Numero piloto: {driver.driver_number}</h4>
  <h4>Pais: {driver.country_code}</h4>
</div>

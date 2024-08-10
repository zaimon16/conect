<script>
  import Pilotos from "./lib/Pilotos.svelte";

  let Drivers = [];
  let datosApi;
  let session = 1;

  const listenInput = (event) => session = event.target.value

  async function infoPilotos() {
    const response = await fetch(
      "https://api.openf1.org/v1/drivers?driver_number=" + session + "&session_key=latest"
    );
    if (!response.ok) {
      throw new Error(`Error API ${response.status}`);
    }
    datosApi = await response.json();
    Drivers = datosApi;
    console.log(datosApi);
  }



  infoPilotos();

  function Siguiente() {
    session++;
    infoPilotos();
  }

  function Anterior() {
    session--;
    infoPilotos();
  }
</script>

<body id="body">
  <header id="head"><h1>F1 API</h1></header>
  <main>
    <div>
      <input
        id="buscador"
        type="text"
        value={session}
        placeholder="Buscar numero Piloto"
        on:input={listenInput}
      />

      <div id="buscadores">
<button id="personajes">Buscar</button>
      </div>
    </div>

    <div id="driverinfo">
      {#each Drivers as driver}
        <Pilotos {driver} />
      {/each}
    </div>

    <div id="buscadores">
      <button id="personajes" on:click={Anterior}>Anterior</button>
      <button id="personajes" on:click={Siguiente} disabled={session === 9158}>Siguiente</button>
    </div>

    <div></div>
  </main>
</body>

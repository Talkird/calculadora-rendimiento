<script lang="ts">
  let ars0 = 0;
  let interest = 0;
  let usd0 = 0;
  let usdf = 0;
  let rendimiento = 0;
  let total = 0;

  const calculate = () => {
    const totalUsd = (ars0 * (1 + interest / 100)) / usdf;
    const usdInicial = ars0 / usd0;
    total = parseFloat((totalUsd - usdInicial).toFixed(2));

    rendimiento = 100 * (total / usdInicial);
    rendimiento = parseFloat(rendimiento.toFixed(2));
  };

  const handleKeyDown = (event: KeyboardEvent) => {
    if (event.code === "Enter") {
      event.preventDefault();
      calculate();
    }
  };

  window.addEventListener("keydown", handleKeyDown);
</script>

<main class="h-screen flex items-center justify-center p-6 bg-base-200">
  <div class="card w-full max-w-lg shadow-lg bg-base-100 p-8">
    <h1 class="text-4xl font-semibold text-primary mb-6 text-center">
      Calculadora de Rendimiento
    </h1>

    <div class="flex flex-col gap-6">
      <div>
        <span class="label">Inicial ARS</span>
        <input
          bind:value={ars0}
          type="text"
          placeholder="Ingrese el monto inicial en ARS"
          class="input input-bordered input-lg w-full"
        />
      </div>

      <div>
        <span class="label">Precio Inicial USD</span>
        <input
          bind:value={usd0}
          type="text"
          placeholder="Ingrese el precio inicial en USD"
          class="input input-bordered input-lg w-full"
        />
      </div>

      <div>
        <span class="label">Tasa de Interés (%)</span>

        <input
          bind:value={interest}
          type="text"
          placeholder="Ingrese la tasa de interés"
          class="input input-bordered input-lg w-full"
        />
      </div>

      <div>
        <span class="label">Precio Final USD</span>

        <input
          bind:value={usdf}
          type="text"
          placeholder="Ingrese el precio final en USD"
          class="input input-bordered input-lg w-full"
        />
      </div>

      <button
        on:click={calculate}
        class="btn btn-primary btn-lg mt-4 w-full hover:scale-105 transition-all duration-300"
      >
        Calcular
      </button>

      {#if rendimiento !== 0 && !Number.isNaN(rendimiento)}
        <div
          class="text-xl text-center mt-6 flex flex-col gap-2 p-4 bg-base-300/50 rounded-lg"
        >
          {#if rendimiento > 0}
            <p>
              Rendimiento: <span class="text-success font-semibold"
                >{rendimiento}%</span
              >
            </p>
            <p>
              Ganancia: <span class="text-success font-semibold"
                >{total.toFixed(2)} USD</span
              >
            </p>
          {:else}
            <p>
              Rendimiento: <span class="text-error font-semibold"
                >{rendimiento}%</span
              >
            </p>
            <p>
              Pérdida: <span class="text-error font-semibold"
                >{total.toFixed(2)} USD</span
              >
            </p>
          {/if}
        </div>
      {/if}
    </div>
  </div>
</main>

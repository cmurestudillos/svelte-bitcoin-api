<script>
    import { onMount } from 'svelte';
    // Peticiones Http
    import axios from 'axios';
  
    let activeTab = 1;

    let apiEur = 'https://api.coindesk.com/v1/bpi/currentprice/EUR.json';
    let apiUsd = 'https://api.coindesk.com/v1/bpi/currentprice/USD.json';
    let apiGbp = 'https://api.coindesk.com/v1/bpi/currentprice/GBP.json';
    let modenaEur = [];
    let modenaUsd = [];
    let modenaGbp = [];
  
    onMount(() => {
        // Llamamos al metodo Euro
        getEurCurerency();
        // Llamamos al metodo Dolares
        getUsdCurerency();
        // Llamamos al metodo Libras
        getGbpCurerency();        
    });
  
    function changeTab(tabNumber) {
      activeTab = tabNumber;
    }

    function getEurCurerency() {
        axios.get(apiEur)
            .then( res => {
                if(res.data){
                modenaEur = res.data['bpi'].EUR;
            }
        });
    };

    function getUsdCurerency() {
        axios.get(apiUsd)
            .then( res => {
                if(res.data){
                modenaUsd = res.data['bpi'].USD;
            }
        });
    };

    function getGbpCurerency() {
        axios.get(apiGbp)
            .then( res => {
                if(res.data){
                modenaGbp = res.data['bpi'].GBP;
            }
        });
    };

  </script>
  
  <div class="tab-container">
    <div class="tab" on:click={() => changeTab(1)} on:keydown={() => {}} class:active={activeTab === 1}>
        {modenaEur.description}
    </div>
    <div class="tab" on:click={() => changeTab(2)} on:keydown={() => {}} class:active={activeTab === 2}>
        {modenaUsd.description}
    </div>
    <div class="tab" on:click={() => changeTab(3)} on:keydown={() => {}} class:active={activeTab === 3}>
        {modenaGbp.description}
    </div>
  </div>
  
  {#if activeTab === 1}
    <div class="tab-content">
        <!-- Contenido de la Tab 1 -->
        <p><img src="../../assets/img/euro.png" width="150" height="150" alt="{modenaEur.description}" title="{modenaEur.description}"></p>
        <p><strong>Valor:</strong> {modenaEur.rate}</p>
    </div>
  {/if}
  
  {#if activeTab === 2}
    <div class="tab-content">
      <!-- Contenido de la Tab 2 -->
      <p><img src="../../assets/img/dollar.png" width="150" height="150" alt="{modenaUsd.description}" title="{modenaUsd.description}"></p>
      <p><strong>Valor:</strong> {modenaUsd.rate}</p>
    </div>
  {/if}
  
  {#if activeTab === 3}
    <div class="tab-content">
      <!-- Contenido de la Tab 3 -->
      <p><img src="../../assets/img/libra.png" width="150" height="150" alt="{modenaGbp.description}" title="{modenaGbp.description}"></p>
      <p><strong>Valor:</strong> {modenaGbp.rate}</p>
    </div>
  {/if}
  